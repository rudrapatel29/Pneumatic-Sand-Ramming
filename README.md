## Pneumatic-Sand-Ramming
This repository contains the code for Pneumatic Ramming Machine project.
# Code
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# Function to calculate force exerted by pneumatic cylinder
def calculate_force(pressure, diameter):
    radius = diameter / 2
    area = np.pi * (radius ** 2)
    force = pressure * area
    return force

# Taking input from the user
diameter = float(input("Enter the diameter of the pneumatic cylinder (in meters): "))  # in meters
pressure = float(input("Enter the operating pressure of the pneumatic cylinder (in MPa): ")) * 10**6  # in Pascals

# Force Calculation
force = calculate_force(pressure, diameter)

# Given force and hardness values for the plot
force_values = [200, 225, 250, 275]
hardness_values = [55.68, 62.12, 68.74, 73.28]

# Plotting
plt.figure(figsize=(10, 6))
plt.plot(force_values, hardness_values, marker='o', linestyle='-', color='b')

# Adding titles and labels
plt.title('Mold Hardness vs. Applied Force')
plt.xlabel('Force (Newtons)')
plt.ylabel('Mold Hardness (Shore A)')
plt.xticks(np.arange(200, 280, 25))
plt.yticks(np.arange(55, 80, 5))
plt.grid(True)

# Annotating data points
for i, (force, hardness) in enumerate(zip(force_values, hardness_values)):
    plt.annotate(f'({force}, {hardness})', (force, hardness), textcoords="offset points", xytext=(0,10), ha='center')

# Displaying the plot
plt.show()

# Detailed Analysis
print("Force Calculation Details:")
print(f"Cylinder diameter: {diameter * 1000} mm")
print(f"Operating pressure: {pressure / 10**6} MPa")
print(f"Calculated force: {force:.2f} N\n")

for f, hardness in zip(force_values, hardness_values):
    print(f"For a force of {f} Newtons, the mold hardness is {hardness} Shore A.")

# Linear regression to understand the relationship
coefficients = np.polyfit(force_values, hardness_values, 1)

# Printing linear regression details
print("\nLinear Regression Analysis:")
print(f"Hardness = {coefficients[0]:.2f} * Force + {coefficients[1]:.2f}")

# Predicting hardness for an example force
example_force = 250
predicted_hardness = np.poly1d(coefficients)(example_force)
print(f"\nPredicted hardness for a force of {example_force} Newtons is {predicted_hardness:.2f} Shore A.\n")

# Displaying table
data = {
    'Force (Newtons)': force_values,
    'Mold Hardness (Shore A)': hardness_values
}

df = pd.DataFrame(data)
print("Mold Hardness vs. Applied Force Table:")
print(df)

![image](https://github.com/rudrapatel29/Pneumatic-Sand-Ramming/assets/155883068/00809077-3ab8-4953-9e77-e34684251706)
