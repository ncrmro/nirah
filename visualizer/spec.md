## Project 1: Interplanetary Radio Signal Visualizer (The "Signal" Project)

### 1.1 Purpose & Scope

To create a simulation tool that visualizes the electromagnetic propagation of radio signals from a terrestrial origin point to target celestial bodies (e.g., Mars, Moon, Voyager probes) in real-time. The system must account for the speed of light, planetary positioning, and the user’s physical location.

### 1.2 Functional Requirements

#### **FR-1: Solar System Simulation**

* **FR-1.1:** The system shall maintain an accurate, scale-model representation of the solar system, including the Sun, Earth, Moon, and target planets/satellites.
* **FR-1.2:** The system shall update celestial body positions in real-time based on standard ephemeris data (e.g., current date/time).
* **FR-1.3:** The system shall support a "floating origin" coordinate system to handle the massive scale difference between human-scale distances (meters) and astronomical distances (Au) without rendering jitter.

#### **FR-2: Signal Propagation Physics**

* **FR-2.1:** The system shall allow the user to trigger a "Transmission Event" from a specific geographic coordinate on Earth.
* **FR-2.2:** The system shall visualize the signal wavefront propagating at the speed of light ( m/s).
* **FR-2.3:** The visualization shall represent the signal as an expanding spherical volume or directional beam, depending on user selection.
* **FR-2.4:** The system shall calculate and display "Time of Flight" (light-minutes/hours) for the signal to reach the selected target.

#### **FR-3: User Interaction & Augmented Reality (AR)**

* **FR-3.1:** The system shall request access to the user's geolocation (Latitude/Longitude/Altitude).
* **FR-3.2:** The system shall provide a "Camera Overlay Mode" (AR) that aligns the virtual camera with the device's physical orientation (IMU data).
* **FR-3.3:** In Camera Overlay Mode, the system shall visually overlay the true position of the target planet in the sky, even if occluded by the Earth (e.g., rendering "through the ground").

### 1.3 Data Requirements

* **Ephemeris Data:** High-precision orbital parameters for celestial bodies.
* **Geospatial Data:** WGS84 ellipsoid or similar reference system for Earth coordinates.

---

## Project 2: 3D Graph & Version Control Explorer (The "Repo" Project)

### 2.1 Purpose & Scope

To create a high-performance 3D visualization engine capable of rendering complex Directed Acyclic Graphs (DAGs), specifically optimized for analyzing Version Control System (VCS) history and software dependency trees.

### 2.2 Functional Requirements

#### **FR-4: Data Ingestion & Parsing**

* **FR-4.1:** The system shall accept data input from standard Version Control Systems (e.g., Git repositories) or generic JSON/Graph formatted data.
* **FR-4.2:** For VCS data, the system shall extract discrete entities including: Commits, Branches, Tags, Authors, and File Changes.
* **FR-4.3:** The system must be capable of parsing "Headless" or "Bare" repositories without requiring a checked-out working directory.

#### **FR-5: 3D Layout & Rendering**

* **FR-5.1:** The system shall render distinct 3D geometric nodes for each data entity (e.g., Spheres for commits, Cubes for files).
* **FR-5.2:** The system shall render directional edges (lines/curves) representing relationships (e.g., Parent -> Child commit, Branch divergence).
* **FR-5.3:** The system shall apply a physics-based or deterministic layout algorithm (e.g., Force-Directed Graph) to spatially distribute nodes to minimize occlusion and visual clutter.
* **FR-5.4:** The system shall support "Level of Detail" (LOD) rendering to maintain performance when visualizing graphs exceeding 10,000 nodes.

#### **FR-6: Querying & Filtering**

* **FR-6.1:** The system shall provide a search interface to query nodes by attribute (e.g., "Find all commits by Author X").
* **FR-6.2:** The system shall allow users to visually filter the graph (e.g., "Hide all merged branches," "Show only files changed in the last 7 days").
* **FR-6.3:** The system shall support interactive selection, where clicking a node displays detailed metadata (Commit Hash, Message, Diff Stats) in a secondary UI panel.
