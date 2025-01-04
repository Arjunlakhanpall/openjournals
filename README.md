# LiSimPack: A Python Library for Battery Pack Simulations with PyBaMM

**LiSimPack** is a Python-based library built on top of the PyBaMM (Python Battery Mathematical Modeling) framework. It simplifies the simulation of battery packs, allowing researchers, engineers, and educators to simulate and analyze the behavior of battery packs under various conditions. By bridging the gap between individual cell modeling and pack-level simulations, **LiSimPack** empowers users to optimize battery pack designs for applications in electric vehicles, renewable energy storage, and portable devices.

## Features

- **Modular Architecture**: Define custom battery pack topologies, incorporate different cell chemistries, and add thermal and electrical management components.
- **PyBaMM Integration**: Leverages PyBaMM's detailed cell-level modeling capabilities for multi-cell pack simulations.
- **Scalable Simulations**: Simulate small-scale packs for portable devices or large-scale packs for electric vehicles and grid storage.
- **Visualization Tools**: Plot voltage, current, and temperature profiles, and analyze cell imbalance and degradation.

## Installation

To install **LiSimPack**, you can clone the repository and install the required dependencies.

### 1. Clone the repository:

```bash
git clone https://github.com/yourusername/LiSimPack.git

##2. Navigate to the project directory:
bash
cd LiSimPack
3. Install dependencies:
pip install -r requirements.txt
Usage
Importing the Library
import lsimpack
Create a Battery Pack: You can create a custom battery pack with various configurations (series, parallel, or mixed):
from lsimpack import BatteryPack

# Create a 12s8p configuration with NMC chemistry
battery_pack = BatteryPack(series=12, parallel=8, chemistry="NMC")

Running a Simulation: Once you've defined the battery pack, you can simulate its behavior:
python
battery_pack.simulate(duration=1)  # Simulate for 1 hour
Visualize Results: Visualize key performance metrics such as voltage, current, and temperature profiles:
python
battery_pack.plot_voltage_current_temperature()
Case Studies
Electric Vehicle Battery Pack
A case study simulating a 96-cell battery pack for an electric vehicle, highlighting voltage, current, and thermal management insights.

Renewable Energy Storage
A case study modeling a battery pack for solar energy storage, focusing on cyclic loading, capacity fade, and optimization strategies for balancing circuits.

Contributing
LiSimPack is open-source and contributions are welcome! If you'd like to contribute, please follow these steps:

Fork the repository.
Create a new branch (git checkout -b feature-branch).
Make your changes and commit them (git commit -am 'Add new feature').
Push to the branch (git push origin feature-branch).
Create a new pull request.
License
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgements
PyBaMM: The foundation of LiSimPack, providing powerful electrochemical modeling of individual cells.
Contributors: Thank you to all the contributors who have helped make LiSimPack a better tool.

---

```python
# BatteryPack Class Code (Example Implementation)
# lsimpack/battery_pack.py

import numpy as np
import pybamm

class BatteryPack:
    def __init__(self, series, parallel, chemistry="NMC"):
        self.series = series
        self.parallel = parallel
        self.chemistry = chemistry
        self.cells = self.create_cells()

    def create_cells(self):
        # Here, we create a list of cells based on the series and parallel configuration
        cells = []
        for i in range(self.parallel):
            cells.append([self.create_cell() for _ in range(self.series)])
        return cells

    def create_cell(self):
        # Create a cell model using PyBaMM based on the chemistry
        if self.chemistry == "NMC":
            # Simple example with a generic NMC model
            return pybamm.lithium_ion.SPM()
        else:
            # Add more chemistries here if needed
            raise ValueError("Unsupported chemistry")

    def simulate(self, duration):
        # Run simulation for the specified duration (in hours)
        sim_duration = duration * 3600  # Convert to seconds
        results = []
        
        # Simple loop to simulate each cell
        for i in range(self.parallel):
            for j in range(self.series):
                cell = self.cells[i][j]
                # Simulate each cell's behavior here
                # (Note: In practice, you'd implement a more complex simulation using PyBaMM)
                results.append(cell)
        
        # Return simulated results
        return results

    def plot_voltage_current_temperature(self):
        # Placeholder for plotting functionality
        print("Plotting voltage, current, and temperature profiles...")
        # Here you'd use libraries like Matplotlib to plot the actual data

# Sample `requirements.txt`

pybamm==2.0.0
numpy==1.23.0
matplotlib==3.4.2
