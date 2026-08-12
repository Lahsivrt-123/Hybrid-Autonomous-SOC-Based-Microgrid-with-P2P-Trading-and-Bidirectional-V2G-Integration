# Autonomous SOC-Based Communication-Free Microgrid with P2P Trading and Bidirectional V2G Integration

> Research Project \| Hybrid Microgrid \| Decentralized Energy
> Management \| P2P Energy Sharing \| V2G

## Overview

This project explores an autonomous hybrid microgrid architecture
designed to coordinate distributed energy resources without making
communication infrastructure a mandatory dependency for basic energy
sharing.

The proposed system combines:

-   Solar PV and wind generation
-   Battery energy storage with SOC-based management
-   Five prosumer nodes and five consumer nodes
-   Local BMS and PLC-based operating decisions
-   Inverter-based droop coordination
-   Communication-independent P2P energy sharing
-   Bidirectional Vehicle-to-Grid (V2G)
-   Critical-load protection for applications such as hospitals
-   Grid-connected and islanded operating scenarios

The central idea is:

> **Instead of requiring a central controller to command every energy
> transaction, the system aims to allow connected nodes to respond
> autonomously to the electrical operating condition of the common
> bus.**

Communication may still be used for monitoring, logging and telemetry,
but the intended fundamental energy-sharing mechanism should not depend
on it.

## Problem Statement

Conventional microgrid architectures can coordinate solar, storage, EVs
and loads using supervisory controllers, SCADA systems and communication
networks. These approaches provide extensive monitoring and
optimization, but can also introduce additional infrastructure,
complexity and communication dependencies.

This project investigates:

> **Can distributed energy resources share power autonomously through
> local decisions and the electrical network itself, while reducing
> dependence on centralized communication for fundamental energy
> coordination?**

The project is particularly targeted toward MSME-scale facilities, rural
and remote applications, educational campuses, healthcare facilities and
other sites where resilient local operation is valuable.

## Proposed Architecture

``` text
                    GRID
                      |
              COMMON MICROGRID BUS
                      |
      +---------------+---------------+
      |               |               |
  Prosumer 1      Prosumer 2      Prosumer 3
 PV+Wind+BESS    PV+Wind+BESS    PV+Wind+BESS
      |               |               |
      +---------------+---------------+
                      |
          +-----------+-----------+
          |           |           |
      Consumers    EVCS/V2G   Critical Load
       C1...C5                 Hospital
                      |
                 Prosumer 4/5
```

Each prosumer node is intended to contain:

``` text
PV / Wind
    |
    v
MPPT / Power Conversion
    |
    v
Battery
    |
    v
BMS
    +---------> Local PLC
                    |
                    v
                Contactors
    |
    v
Inverter
    |
    v
Droop / Local Power Control
    |
    v
Common Electrical Bus
```

## Role of Each Control Layer

### BMS

Provides battery-related information such as:

-   State of Charge (SOC)
-   Battery availability
-   Protection status
-   Fault/alarm conditions
-   Charging/discharging limits

### PLC

The PLC is the local supervisory controller. It is not intended to
continuously control inverter switching.

Its role is to:

-   Read local BMS status
-   Apply SOC and protection rules
-   Determine the local operating state
-   Control contactors
-   Enable/disable inverter operation
-   Handle local startup, shutdown and isolation sequences

The proposed industrial implementation identifies a Siemens S7-1200 PLC.

### Contactors

Contactors provide the physical connection/isolation mechanism.

``` text
BMS -> PLC -> Contactor -> Node connected / isolated
```

### Inverter

The inverter interfaces stored energy with the microgrid and implements
local power-control behaviour.

### Droop Control

Droop control is intended to operate at the inverter/control layer.
Connected inverters respond to the electrical operating condition of the
common bus according to their local control characteristics.

The electrical network therefore becomes the physical coupling mechanism
for power sharing.

## Communication-Free Energy Sharing

"Communication-free" refers specifically to the intended fundamental
energy-sharing mechanism.

It does not mean the complete system can never contain communication.
Communication may still be used for:

-   Monitoring
-   Data logging
-   Telemetry
-   Diagnostics
-   Remote dashboards
-   Higher-level optimization

The objective is that loss of supervisory communication should not
necessarily prevent fundamental local energy-sharing and protection
functions.

## Existing Simulation Work

A detailed MATLAB/Simulink/Simscape model has been developed as the
electrical-system foundation.

The model includes:

-   PV generation
-   Wind generation
-   Battery storage
-   Power converters
-   PWM generation
-   Three-phase electrical systems
-   PLL-based synchronization
-   Loads
-   Grid connection
-   Breakers
-   Three-phase fault modelling
-   Consumer-side energy-management logic
-   EVCS/V2G infrastructure
-   SOC-based control logic
-   Measurement and data logging

The existing model contains explicit rule-based control and
energy-routing logic. The proposed MSME development takes this
foundation further by redesigning the coordination layer toward local
BMS/PLC decisions, inverter droop coordination and common-bus-based
power sharing.

## Embedded Prototype

A reduced-scale embedded prototype has been explored using:

-   ESP32
-   INA219 sensing
-   Relay/contactors
-   FreeRTOS-based task scheduling
-   MQTT/Wi-Fi telemetry

The embedded prototype is intended to validate local embedded-control
concepts before moving toward industrial PLC/BMS implementation.

## V2G Integration

Bidirectional Vehicle-to-Grid operation is included as an additional
distributed energy-storage resource.

``` text
        EV
         |
   +-----+-----+
   |     |     |
Charge  Idle  Discharge
Absorb         Supply
Power          Power
```

V2G provides additional flexibility when EVs are parked and available
for controlled charging/discharging.

## Critical Load Protection

Critical loads such as hospital loads are treated separately from
ordinary consumers. The intended design includes an independent
protection path so that critical-load protection is not solely dependent
on software or supervisory communication.

The current simulation represents the hospital load and
protection-related infrastructure; the dedicated industrial hardware
implementation is part of the proposed development work.

## Technology Stack

### Simulation

-   MATLAB
-   Simulink
-   Simscape Electrical

### Embedded Prototype

-   ESP32
-   FreeRTOS
-   INA219
-   Relay/contactors
-   MQTT/Wi-Fi telemetry

### Proposed Industrial Hardware

-   Siemens S7-1200 PLC
-   Industrial BMS
-   LiFePO4 battery
-   Victron SmartSolar MPPT
-   Victron MultiPlus inverter
-   Schneider contactors

### Control

-   SOC-based energy management
-   MPPT
-   Inverter control
-   Droop-based coordination
-   P2P energy sharing
-   V2G
-   Protection and isolation
-   Islanding/reconnection

## Development Roadmap

### Stage 1 --- Existing Foundation

Validate the detailed five-node hybrid microgrid simulation.

### Stage 2 --- Decentralized Control

Replace explicit energy-routing decisions with local node-level control
and inverter-based droop coordination.

### Stage 3 --- Three-Node Prototype

Validate:

-   Bus-voltage stability
-   Power-sharing behaviour
-   SOC response
-   Response time
-   Protection behaviour

### Stage 4 --- Five-Node Prototype

Expand the validated architecture to five prosumer/consumer nodes.

### Stage 5 --- V2G Integration

Add bidirectional EV charging/discharging.

### Stage 6 --- Critical Load Protection

Integrate the dedicated critical-load protection mechanism.

### Stage 7 --- Industrial Implementation

Migrate the validated architecture toward:

**BMS -\> Siemens S7-1200 PLC -\> Contactors -\> Industrial inverter**

## Key Performance Indicators

  KPI                     Purpose
  ----------------------- ---------------------------------------------
  Bus Voltage Deviation   Evaluate electrical stability
  Power-Sharing Error     Measure effectiveness of power sharing
  Response Time           Measure reaction to load/generation changes
  Battery SOC             Verify operating limits
  Renewable Utilization   Evaluate renewable-energy use
  Energy Exchanged        Quantify P2P energy transfer
  Protection Response     Verify safe isolation

## Target Applications

-   MSME manufacturing units
-   Agro-industrial facilities
-   Rural healthcare centres
-   Educational campuses
-   Commercial buildings
-   Remote installations
-   Distributed renewable-energy clusters

## Project Positioning

This project does not claim that individual technologies such as
batteries, droop control, PLCs, V2G or SOC-based management are new.

The research focus is the system-level integration of these established
technologies into an autonomous, MSME-oriented architecture.

The intended contribution is to investigate whether:

> **A distributed microgrid can maintain basic energy-sharing and local
> protection functions through local decisions and electrical coupling,
> without making centralized communication a mandatory dependency for
> every energy transaction.**

## Repository Structure

``` text
/
├── README.md
├── Simulink/
│   ├── models/
│   └── results/
├── ESP32/
│   ├── src/
│   └── include/
├── Control/
│   ├── MPPT/
│   ├── SOC_Management/
│   ├── Droop_Control/
│   ├── P2P_Energy_Sharing/
│   └── V2G/
├── Hardware/
│   ├── Schematics/
│   ├── Wiring/
│   └── BOM/
└── Documentation/
    ├── Architecture/
    ├── Test_Results/
    └── Reports/
```

## Project Status

**Research / Prototype Development**

### Existing

-   Detailed five-node Simulink/Simscape hybrid microgrid model
-   PV and wind generation modelling
-   Battery and SOC-based control
-   Consumer-side energy-management logic
-   EVCS/V2G modelling
-   Fault and protection infrastructure
-   Reduced-scale ESP32-based embedded-control work

### Under Development

-   Decentralized droop-based P2P coordination
-   Three-node experimental validation
-   Five-node hardware implementation
-   Industrial PLC/BMS integration
-   V2G experimental validation
-   Critical-load hardware protection

## Research Question

> **Can local SOC-aware controllers and inverter-based electrical
> coordination provide stable and reliable peer-to-peer energy sharing
> in a multi-node hybrid microgrid without requiring a central
> communication network for fundamental power coordination?**

------------------------------------------------------------------------

**Institution:** Chennai Institute of Technology\
**Domain:** Electrical & Electronics Engineering\
**Focus:** Hybrid Microgrids \| Smart Energy Management \| P2P Energy
Sharing \| V2G \| Renewable Energy
