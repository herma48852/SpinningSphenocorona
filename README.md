# Enhanced Sphenocorona (Johnson Solid J86) Visualizer

## Overview

This project is an interactive 3D visualizer for the Sphenocorona, also known as Johnson solid J86. The sphenocorona is a convex polyhedron with 14 faces (12 triangles and 2 squares), 22 edges, and 10 vertices. This enhanced tool calculates its geometric properties from the root of a polynomial and renders it using Three.js, allowing for comprehensive interactive exploration of the polyhedron's structure through multiple, combinable separation modes.

All detailed calculations, vertex coordinates, edge lists, and geometric property verifications are output to the browser's developer console upon loading.

## Features

### **Accurate Geometric Calculation**
* Calculates the unique real root `k` of the polynomial `60x⁴ - 48x³ - 100x² + 56x + 23 = 0`.
* Computes the 10 vertex coordinates for a unit edge length sphenocorona based on the value of `k`.
* Identifies the 22 edges and 14 faces connecting these vertices.

### **Interactive 3D Visualization**
* Rendered using Three.js with custom mouse controls.
* **Spinning Animation:** The model automatically rotates on two axes.
  * **Pause/Resume Control:** A button to pause or resume the animation.
  * **Speed Control:** A slider to adjust the rotation speed.
* **Custom Mouse Controls:**
  * **Rotate:** Left-click and drag to orbit the camera around the model.
  * **Pan:** Right-click and drag to shift the camera's view.
  * **Zoom:** Use the mouse scroll wheel to zoom in and out.

### **Flexible, Combinable Separation System**
The visualizer features an independent control system allowing any combination of the four separation modes to be active at once. The transformations are cumulative.

* **Separate Squares (Indiv.):** Separates the two square faces `(0,1,5,4)` and `(2,3,5,4)` from the main body, each moving outward along its own normal vector.
* **Separate Connected Squares:** Treats the two square faces as a single, connected unit and separates them from the main body along the axis defined by the midpoints of edges `(8,9)` and `(0,1)`.
* **Separate Triangles:** Separates the two opposing triangular faces `(4,5,9)` and `(2,3,8)`, each moving outward along its own normal vector.
* **Separate Pyramids:** Splits the sphenocorona into its three core components: two pentagonal pyramids and the central wedge.
  * Pyramid 1, capped by vertex 7, moves in the positive direction along the axis defined by vertices 6 and 7.
  * Pyramid 2, capped by vertex 6, moves in the negative direction along the same axis.

### **Display Modes**
* **Solid & Wireframe:** Toggle between a solid-shaded view and a wireframe representation.
* **Face Coloring (Solid Mode Only):**
  * **Multi-Color Mode:** Assigns distinct colors to adjacent faces using a greedy algorithm.
  * **Monochrome Mode:** Uses a default color for the main body and distinct, hardcoded colors for each of the separable components.
* **Sharp Edge Delineation:** Contrasting line overlay for clear face separation in solid mode.

### **Vertex Labels**
* Numerical labels (0-9) displayed at each vertex using an HTML overlay system.
* **Smart Following:** Labels are dynamically assigned to the most relevant moving face group, ensuring they correctly track their corresponding vertex through all combined separation states and model rotations.
* **Occlusion Detection:** Labels are automatically hidden when they are blocked by solid geometry from the camera's perspective.

### **Smooth Animations**
* All transitions between separation states are smoothly animated using linear interpolation (lerp).
* The system supports simultaneous, independent animations for each separation mode.

## How to Use

1. **Open the HTML File:** Open the `index.html` file in a modern web browser that supports WebGL (e.g., Chrome, Firefox, Safari, Edge).
2. **Automatic Load:** The visualization and calculations begin automatically when the page loads.
3. **Check Console for Data:** Open your browser's developer console (F12) to view the calculated root `k`, vertex coordinates, and other geometric details.
4. **Interact with Controls:**
   * Use the buttons and slider in the control panel to manipulate the visualization.
   * Activate any combination of the four separation toggles to explore the model's components.
5. **Navigate the 3D View:**
   * **Rotate:** Left-click and drag.
   * **Pan:** Right-click and drag.
   * **Zoom:** Mouse scroll wheel.

## Technical Details

### **Mathematical Foundation**
* Vertex coordinate calculations are based on the established method of finding the root `k` of the polynomial `60x⁴ - 48x³ - 100x² + 56x + 23 = 0`.
* This method is referenced in various mathematical resources for Johnson solids.

### **Technologies Used**
* **HTML5** for structure.
* **CSS3** (including Tailwind CSS via CDN) for styling.
* **JavaScript (ES6+)** for calculations, logic, and DOM manipulation.
* **Three.js (r128 via CDN)** for WebGL-based 3D rendering.
* **Custom HTML overlay system** for dynamic vertex labels.

### **Architecture**
* **Component-Based Model:** The sphenocorona is constructed from 14 individual `THREE.Group` objects, one for each face. This allows for maximum flexibility in applying transformations.
* **Independent State Management:** Each of the four separation modes is controlled by its own set of boolean state variables and animation lerp factors.
* **Cumulative Transformations:** In each animation frame, the final position of every face group is calculated by cumulatively applying the transformations from all active separation modes.
* **Dynamic Label Hosting:** The logic for vertex labels dynamically determines the most appropriate host face for each label in every frame, prioritizing faces that are part of an active separation to ensure smooth and accurate tracking.

## Geometric Structure and Separation Definitions

### **Key Components**
* **Square 1:** Face `(0,1,5,4)`
* **Square 2:** Face `(2,3,5,4)`
* **Triangle 1:** Face `(4,5,9)`
* **Triangle 2:** Face `(2,3,8)`
* **Pyramid 1 (capped by V7):** Comprised of faces `(1,5,7)`, `(5,9,7)`, `(9,8,7)`, `(8,3,7)`, and `(3,1,7)`.
* **Pyramid 2 (capped by V6):** Comprised of faces `(0,2,6)`, `(2,8,6)`, `(8,9,6)`, `(9,4,6)`, and `(4,0,6)`.
* **Main Body / Wedge:** All other faces not part of the defined pyramids.

### **Separation Axes**
* **Individual Squares & Triangles:** Each separates along its own calculated face normal.
* **Connected Squares:** Separates along the axis from the midpoint of edge `(8,9)` to the midpoint of edge `(0,1)`.
* **Pyramids:** Separates along the axis defined by the vector from vertex 6 to vertex 7.

## Browser Compatibility

Requires a modern web browser with WebGL support:
* Chrome 60+
* Firefox 55+
* Safari 12+
* Edge 79+

## Files

* Single self-contained HTML file with embedded CSS and JavaScript.
* No external dependencies except Three.js and Tailwind CSS, both loaded via CDN.
