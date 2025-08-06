import random
import time

class Battery:
    def __init__(self):
        self.soc = 100  # State of Charge in %
        self.voltage = 4.2  # Voltage in Volts
        self.temperature = 25  # Temperature in °C
        self.health = 100  # Battery Health in %
        self.cycles = 0

    def update_conditions(self):
        # Simulate discharge
        discharge_rate = random.uniform(0.1, 1.0)
        self.soc = max(0, self.soc - discharge_rate)

        # Simulate voltage drop
        self.voltage = max(3.0, 3.0 + (self.soc / 100) * 1.2)

        # Simulate temperature changes
        self.temperature += random.uniform(-0.5, 0.5)
        self.temperature = max(10, min(60, self.temperature))

        # Simulate battery degradation
        if self.soc == 0:
            self.cycles += 1
            self.health -= random.uniform(0.1, 0.5)
            self.soc = 100  # Simulate recharge

        self.health = max(50, self.health)

    def get_status(self):
        return {
            "State of Charge (%)": round(self.soc, 2),
            "Voltage (V)": round(self.voltage, 2),
            "Temperature (°C)": round(self.temperature, 2),
            "Battery Health (%)": round(self.health, 2),
            "Charge Cycles": self.cycles
        }


# --- Simulation Loop ---
battery = Battery()

for i in range(20):  # Simulate 20 time steps
    battery.update_conditions()
    status = battery.get_status()

    print(f"\n⏱️ Time Step {i + 1}")
    for key, value in status.items():
        print(f"{key}: {value}")

    time.sleep(0.5)  # Add delay to mimic real-time monitoring

