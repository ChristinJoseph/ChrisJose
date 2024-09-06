# ChrisJose
import serial

# Initialize serial connection to SBUS receiver
sbus = serial.Serial('/dev/ttyUSB0', baudrate=100000, parity=serial.PARITY_EVEN, stopbits=serial.STOPBITS_TWO)

def read_sbus_frame():
    while sbus.in_waiting >= 25:
        data = sbus.read(25)
        if data[0] == 0x0F and data[24] == 0x00:  # Check start and end bytes
            # Extract channel data
            channels = []
            channels.append((data[1] | data[2] << 8) & 0x07FF)    # Channel 1
            # Add more channels as needed
            return channels

def map_sbus_to_pwm(sbus_value):
    # Map SBUS range to PWM range for motor control
    # Assuming SBUS value range: 172 - 1811, PWM range: 1000 - 2000 us
    pwm_value = ((sbus_value - 172) * (2000 - 1000) / (1811 - 172)) + 1000
    return pwm_value

def control_motor(pwm_value):
    # Send PWM signal to Sabertooth driver (using a PWM library or direct GPIO control)
    # Example with pseudo-code:
    # pwm_output.write(pwm_value)
    pass

while True:
    channels = read_sbus_frame()
    if channels:
        motor_pwm = map_sbus_to_pwm(channels[0])  # Use Channel 1 data for Motor 1
        control_motor(motor_pwm)
