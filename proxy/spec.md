This specification outlines the functional requirements for the **Interplanetary Network Gateway (ING)**, a proxy server designed to emulate the physical constraints of deep-space communication for software testing.

---

## Project 1: Interplanetary Network Gateway (ING) Specification

### 1.1 Purpose & Scope

The ING shall act as a **transparent network bridge** between distinct "Service Zones" (e.g., Earth Network, Mars Network). It intercepts network traffic (TCP/UDP/HTTP), applies physics-based constraints—specifically variable light-speed latency, bandwidth throttling, and signal degradation—and forwards it to the destination, effectively "faking" the distance between planets for local applications.

### 1.2 Functional Requirements

#### **FR-1: Zone Management & Topology**

* **FR-1.1:** The system shall allow the definition of **Service Zones** (e.g., "Earth-Ground", "Mars-Orbit", "Europa-Lander").
* **FR-1.2:** Each Zone shall be assigned a specific **Network CIDR** (e.g., Earth: `192.168.1.0/24`, Mars: `10.0.0.0/24`) or a virtual hostname suffix (e.g., `*.mars.local`).
* **FR-1.3:** The system shall maintain a dynamic **Topology Graph** defining which zones have "Line of Sight" connectivity at any given moment, based on external orbital parameters.

#### **FR-2: Physics-Driven Latency Engine**

* **FR-2.1:** The system shall not use static delay values. Instead, it must calculate delay () dynamically using the formula: 

* **FR-2.2:** The system must accept **Ephemeris Updates** (real-time distance data) from an external source (such as the Project 2 Visualization tool) to update  continuously.
* **FR-2.3:** The system must implement a **"Store-and-Forward" buffer** capable of holding data packets for extended periods (from minutes to hours) without timing out the client-side connection (mimicking DTN/Bundle Protocol behavior).

#### **FR-3: Network Address Translation (The "Wormhole" NAT)**

* **FR-3.1:** The system shall provide **Ingress Gateways** for each zone. A service in the "Earth Zone" sends a request to the Gateway (e.g., `localhost:8080`), which maps to a target in the "Mars Zone" (e.g., `10.0.0.5:80`).
* **FR-3.2:** The system shall encapsulate the payload, hold it in the Latency Engine for the duration of the flight time, and then release it from the **Egress Gateway** in the target zone.
* **FR-3.3:** The system must support **Double-NAT** simulation, ensuring that services on "Mars" cannot see the true IP addresses of services on "Earth," only the Proxy's gateway address.

#### **FR-4: Disruption & Error Injection**

* **FR-4.1:** The system shall simulate **Occultation Events**. If a planet blocks the Line of Sight (LoS) between zones, the proxy must drop packets or queue them until LoS is restored (simulating orbital mechanics).
* **FR-4.2:** The system shall simulate **Bit Rot/Packet Corruption** proportional to the distance and "Solar Interference" levels defined in the configuration.
* **FR-4.3:** The system shall cap bandwidth dynamically (e.g., limiting Deep Space Network links to 2 Mbps while Earth links run at 1 Gbps).

#### **FR-5: Telemetry & Visualization Hooks**

* **FR-5.1:** The system shall emit real-time **Telemetry Events** (WebSocket/gRPC) for every packet entering or leaving the simulation pipeline.
* **FR-5.2:** Telemetry data must include: `PacketID`, `SourceZone`, `DestZone`, `ScheduledArrivalTime`, and `CurrentBufferState`.
* *Note: This requirement allows the visualization tool (Project 2) to render the "packet" traveling through space matching the actual network buffer.*



### 1.3 Interface Requirements

* **Control API:** REST/gRPC API to update planetary positions and toggle link failures.
* **Proxy Protocol:** Support for SOCKS5 or HTTP CONNECT tunneling to allow easy integration with standard web browsers and microservices.

### 1.4 Non-Functional Requirements

* **Concurrency:** The system must handle 10,000+ concurrent simulated signal "bundles" efficiently.
* **Time Accuracy:** The internal scheduler must maintain precision within ±10ms of the target release time, regardless of the delay duration (e.g., a 20-minute delay must be accurate to the millisecond).

---

### YouTube Reference

[Simulating Network Latency with speedbump](https://www.youtube.com/watch?v=zb888YxA48w)

*This video demonstrates "Speedbump," a Go-based TCP proxy that introduces variable latency; it serves as an excellent reference implementation for the "Latency Engine" component of your specification.*
