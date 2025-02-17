# Focused Ultrasound Simulation and pMUT Array Design

## Overview

This repository contains Python code for designing, simulating, and visualizing the performance of piezoelectric micromachined ultrasonic transducers (pMUTs) and arrays. The code includes tools for calculating key mechanical and acoustic parameters, visualizing ultrasound fields, and modeling phased array configurations.

The scripts focus on:
- Designing individual pMUT elements with specific material and geometric properties.
- Simulating phased array beamforming to focus ultrasound at a target depth.
- Visualizing directivity patterns and acoustic pressure fields for different array configurations.

## Features

- **pMUT Design**:
  - Define pMUT geometries, materials, and layers.
  - Calculate resonance frequency, stiffness, coupling coefficients, and more.
  - Export layouts to GDSII files for fabrication.

- **Array Design**:
  - Configure arrays with user-defined rows, columns, and pitch.
  - Simulate phase delays for beamforming at specified focal points.

- **Acoustic Simulations**:
  - Visualize ultrasound directivity patterns.
  - Plot acoustic pressure fields and intensity distributions in 2D.

## Installation

This project requires Python 3.8+ and the following libraries:

```bash
pip install numpy scipy sympy matplotlib phidl pandas schemdraw
```

## Usage

### pMUT Design
- Define individual pMUT properties:
  ```python
  my_pmut = Individual_Bipolar_pMUT(
      pMUT_Radius=40e-6,
      Elastic_Material=Silicon_Oxide,
      Piezo_Material=ScAlN(36),
      Medium_Material=Water,
  )
  my_pmut.draw_pMUT()
  ```
- Visualize the layout:
  ```python
  qp(my_pmut.layout)
  ```

### Array Design
- Define and visualize an array:
  ```python
  my_array = Columns_Array(
      Rows=10,
      Columns=20,
      Pitch=250e-6,
      pMUT_Type=my_pmut
  )
  my_array.draw_layout()
  qp(my_array.layout)
  ```

### Focused Ultrasound Simulation
- Simulate and visualize the focused field:
  ```python
  example_array.plot_directivity_function(
      thetas=np.linspace(-np.pi/2, np.pi/2, 300),
      phi=0,
      frequency=500e3,
      farfield=0.05
  )
  ```

## Example: Focal Depth Calculation
The focal depth of an array can be estimated using:
```python
focal_depth = D**2 / (4 * wavelength)
print(f"Focal Depth: {focal_depth:.3f} m")
```

---

### Credits
This project includes components from a GitHub library that was under the MIT license for modeling pMUTs which I have since not been able to find! If you are the owner, please let me know if you took it down so that I can credit you properly.

Enjoy designing your pMUT arrays and simulating focused ultrasound fields! 🎉
