# Interactive Sphenocorona (Johnson Solid J86) Visualizer

## Overview

This project is an interactive 3D visualizer for the Sphenocorona, also known as Johnson solid J86. The sphenocorona is a convex polyhedron with 14 faces (12 triangles and 2 squares), 22 edges, and 10 vertices.

This tool calculates its geometric properties from the root of a polynomial and renders the solid using Three.js. It allows for interactive exploration of the polyhedron's geometry through various controls and separation modes. All detailed calculations and geometric data are output to the browser's developer console upon loading.

## Features

### Accurate Geometric Calculation
* Finds the unique real root `k` of the polynomial `60x⁴ - 48x³ - 100x² + 56x + 23 = 0`.
* Computes the 10 vertex coordinates for a unit edge length sphenocorona based on the value of `k`.
* Identifies the 22 edges and 14 faces (12 triangles, 2 squares) from the vertex data.

### Interactive 3D Visualization
* Rendered using Three.js with custom mouse controls.
* **Spinning Animation:** The model automatically rotates on two axes.
    * **Pause/Resume Control:** A button to pause or resume the animation.
    * **Speed Control:** A slider to adjust the rotation speed.
* **Custom Mouse Controls:**
    * **Rotate:** Left-click and drag to orbit the camera around the model.
    * **Pan:** Right-click and drag to shift the camera's view.
    * **Zoom:** Use the mouse scroll wheel to zoom in and out.

### Display Modes
* **Solid & Wireframe:** Toggle between a solid-shaded view and a wireframe representation.
* **Face Coloring:** In solid mode, toggle between a default monochrome appearance and a multi-color view where adjacent faces have different colors.
* **Vertex Labels:** Numerical labels (0-9) are displayed at each vertex.
    * **Occlusion Culling:** Labels are automatically hidden when they are blocked by the solid model from the camera's perspective.

### Component Separation
* **Separate Square:** A working toggle control to smoothly animate one of the square faces away from the main body along its normal, allowing for inspection of the model's interior.
* **Separate Pyramids (In Progress):** A feature to separate the two pentagonal baseless pyramids (`0,2,8,9,4`) and (`1,5,9,8,3`).

## How to Use

1.  **Open the HTML File:** Open the `index.html` file in a modern web browser that supports WebGL (e.g., Chrome, Firefox, Safari, Edge).
2.  **Interact with Controls:** Use the buttons and slider in the control panel to manipulate the visualization.
3.  **Navigate the 3D View:** Use the mouse controls (left-drag, right-drag, scroll) to change the camera's viewpoint.

## Current Status & To-Do List

This project is fully functional for general visualization and for the "Separate Square" feature. The primary development focus is on fixing the more complex separation of the pentagonal pyramids.

- [x] Implement base polyhedron calculation and rendering.
- [x] Add interactive camera controls and animation.
- [x] Add display mode toggles (solid/wireframe, color/mono, labels on/off).
- [x] Implement occlusion culling for vertex labels.
- [x] **Implement "Separate Square" feature.**
- [ ] **Fix "Separate Pyramids" feature.**
    -   **Current Bug:** When the "Separate Pyramids" feature is activated, only the vertex labels for the pyramids move to their correctly separated positions. The 3D geometry (the faces and edges) of the pyramids remains stationary.
    -   **Path Forward:** The issue likely lies in the scene graph hierarchy or the state management for handling multiple separated pieces. The logic needs to be refactored to correctly update the `position` of the pyramid `THREE.Group` objects within the animation loop, ensuring the geometry transforms along with the labels. The successful architecture used for the "Separate Square" feature should be used as a template.

## Technical Details
* **Frontend:** HTML5, CSS3 (with Tailwind CSS via CDN)
* **3D Rendering:** Three.js (r128 via CDN)
* **Logic:** JavaScript (ES6+)
