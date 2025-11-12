import serial
import time

# Connect to Arduino on COM8
arduino = serial.Serial(port='COM8', baudrate=9600, timeout=1)
time.sleep(2)  # Wait for Arduino to initialize

def send_signal(signal):
    """Send a signal character to Arduino"""
    arduino.write(signal.encode())
    print(f"Signal sent: {signal}")

try:
    while True:
        # Red light ON
        send_signal('R')
        print("🔴 Red ON")
        time.sleep(5)

        # Yellow light ON
        send_signal('Y')
        print("🟡 Yellow ON")
        time.sleep(2)

        # Green light ON
        send_signal('G')
        print("🟢 Green ON")
        time.sleep(5)

        # Green light BLINK (3 times)
        for i in range(3):
            send_signal('G')
            print("🟢 Green BLINK ON")
            time.sleep(0.5)
            send_signal('X')
            print("⚫ Green OFF")
            time.sleep(0.5)

except KeyboardInterrupt:
    print("\nProgram stopped by user.")
    send_signal('X')
    arduino.close()
