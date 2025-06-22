# Enhanced Sphenocorona (Johnson Solid J86) Visualizer

## Overview

This project is an interactive 3D visualizer for the Sphenocorona, also known as Johnson solid J86. The sphenocorona is a convex polyhedron with 14 faces (12 triangles and 2 squares), 22 edges, and 10 vertices. This enhanced tool calculates its geometric properties from the root of a polynomial and renders it using Three.js, allowing for comprehensive interactive exploration of the polyhedron's structure through multiple, combinable separation modes.

All detailed calculations, including vertex coordinates, edge lists, face definitions, and dihedral angles, are performed on load and can be inspected in the browser's developer console.

## Features

### **Accurate Geometric Calculation**
* Calculates the unique real root `k` of the polynomial `60x⁴ - 48x³ - 100x² + 56x + 23 = 0`.
* Computes the 10 vertex coordinates for a unit edge length sphenocorona based on the value of `k`.
* Identifies the 22 edges and 14 faces connecting these vertices.
* Calculates the dihedral angle for each of the 22 edges.

### **Interactive 3D Visualization**
* Rendered using Three.js with custom mouse controls.
* **Spinning Animation:** The model automatically rotates on two axes.
  * **Pause/Resume Control:** A button to pause or resume the animation.
  * **Speed Control:** A slider to adjust the rotation speed. The slider also controls the speed of all separation/join animations, even when spinning is paused.
* **Custom Mouse Controls:**
  * **Rotate:** Left-click and drag to orbit the camera around the model.
  * **Pan:** Right-click and drag to shift the camera's view.
  * **Zoom:** Use the mouse scroll wheel to zoom in and out.

### **Flexible, Combinable Separation System**
The visualizer features an independent control system allowing any combination of the separation modes to be active at once. The transformations are cumulative.

* **Separate Squares (Indiv.):** Separates the two square faces from the main body, each moving outward along its own normal vector.
* **Separate Connected Squares:** Treats the two square faces as a single, connected unit and separates them from the main body.
* **Separate Triangles:** Separates the two opposing triangular faces, each moving outward along its own normal vector.
* **Separate Pyramids:** Splits the sphenocorona into its three core components: two pentagonal pyramids and the central wedge.
* **Separate All:** Separates all 14 faces simultaneously, each moving outward along its own pre-calculated normal vector.

### **Display Modes & Data Labels**
* **Solid & Wireframe:** Toggle between a solid-shaded view and a wireframe representation.
* **Face Coloring (Solid Mode Only):**
  * **Multi-Color Mode:** Assigns distinct colors to adjacent faces using a greedy algorithm.
  * **Monochrome Mode:** Uses a default color for the main body and distinct, hardcoded colors for each of the separable components.
* **Vertex Labels:**
  * Numerical labels (0-9) displayed at each vertex.
  * Smart label tracking ensures labels follow the correct vertex during all separation animations.
  * Labels are automatically hidden when occluded by solid geometry.
* **Dihedral Angle Labels:**
  * Toggle the visibility of the dihedral angle for each of the 22 edges.
  * Angles are displayed in degrees and positioned at the midpoint of each edge.
  * Labels track all model rotations and transformations and are occluded by the solid model.

### **Smooth Animations**
* All transitions between separation states are smoothly animated using linear interpolation (lerp).
* The system supports simultaneous, independent animations for each separation mode, with the speed controlled by the main speed slider.

## How to Use

1.  **Open the HTML File:** Open the `index.html` file in a modern web browser that supports WebGL (e.g., Chrome, Firefox, Safari, Edge).
2.  **Automatic Load:** The visualization and calculations begin automatically when the page loads.
3.  **Interact with Controls:**
    * Use the buttons and slider in the control panel to manipulate the visualization.
    * Activate any combination of the separation toggles to explore the model's components.
    * Toggle the visibility of vertex and dihedral angle labels.
4.  **Navigate the 3D View:**
    * **Rotate:** Left-click and drag.
    * **Pan:** Right-click and drag.
    * **Zoom:** Mouse scroll wheel.

## Technical Details

### **Architecture**
* **Component-Based Model:** The sphenocorona is constructed from 14 individual `THREE.Group` objects, one for each face. This allows for maximum flexibility in applying transformations.
* **Independent State Management:** Each of the five separation modes is controlled by its own set of boolean state variables and animation lerp factors.
* **Cumulative Transformations:** In each animation frame, the final position of every face group is calculated by cumulatively applying the transformations from all active separation modes.
* **Dynamic Label Hosting:** The logic for vertex and dihedral labels dynamically determines the most appropriate host face(s) for each label in every frame, ensuring smooth and accurate tracking through all transformations.

### **Geometric Structure and Separation Definitions**
#### **Key Components**
* **Square 1:** Face `(0,1,5,4)`
* **Square 2:** Face `(2,3,5,4)`
* **Triangle 1:** Face `(4,5,9)`
* **Triangle 2:** Face `(2,3,8)`
* **Pyramid 1 (capped by V7):** Comprised of faces `(1,5,7)`, `(5,9,7)`, `(9,8,7)`, `(8,3,7)`, and `(3,1,7)`.
* **Pyramid 2 (capped by V6):** Comprised of faces `(0,2,6)`, `(2,8,6)`, `(8,9,6)`, `(9,4,6)`, and `(4,0,6)`.
* **Main Body / Wedge:** All other faces not part of the defined pyramids.

#### **Separation Axes**
* **Individual Squares & Triangles:** Each separates along its own calculated face normal.
* **Connected Squares:** Separates along the axis from the midpoint of edge `(8,9)` to the midpoint of edge `(0,1)`.
* **Pyramids:** Separates along the axis defined by the vector from vertex 6 to vertex 7.
* **All Faces:** Each of the 14 faces separates along its own pre-calculated face normal.

## Browser Compatibility
Requires a modern web browser with WebGL support:
* Chrome 60+
* Firefox 55+
* Safari 12+
* Edge 79+

---

## Acknowledgements & Libraries Used
This project utilizes the following open-source libraries:

* **Three.js:** A comprehensive 3D graphics library for creating and displaying animated 3D computer graphics in a web browser.
    * Copyright 2010-2025 Three.js Authors
    * License: MIT
    * Website: [https://threejs.org/](https://threejs.org/)

* **Tailwind CSS:** A utility-first CSS framework for rapidly building custom user interfaces.
    * Copyright © Tailwind Labs Inc.
    * License: MIT
    * Website: [https://tailwindcss.com/](https://tailwindcss.com/)

