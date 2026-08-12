Hybrid Autonomous SOC-Based Microgrid with P2P Trading and Bidirectional V2G Integration

Hybrid Microgrid | SOC-Based Energy Management | P2P EnergySharing | V2G | Autonomous Switching

Overview

This project focuses on the development of an autonomous hybridmicrogrid that combines renewable energy generation, battery energystorage, local SOC-based decision making, peer-to-peer (P2P) energysharing, and bidirectional Vehicle-to-Grid (V2G) integration.

The system is designed around multiple distributed energy nodes that canoperate as producers, consumers, or both. Each node can generate energy,store excess energy in a battery, supply its local load, or participatein energy exchange with other nodes.

The main objective is to develop an energy-management architecture inwhich distributed nodes can make local decisions based on theiravailable generation, load demand, and battery State of Charge (SOC).

Project Objective

The project aims to develop and study a hybrid microgrid capable of:

Managing solar and wind energy

Storing surplus energy in batteries

Monitoring battery State of Charge (SOC)

Automatically switching between available energy sources

Supplying local and neighbouring loads

Enabling peer-to-peer energy exchange

Integrating bidirectional V2G

Maintaining battery operating limits

Supporting grid-connected and islanded operating conditions

Reducing dependence on a single centralized energy source

The long-term goal is to demonstrate how distributed energy resourcescan cooperate through local control and electrical coupling.

System Concept

The proposed architecture consists of multiple prosumer and consumernodes connected through a common electrical network.

                    SOLAR PV
                       |
                    MPPT
                       |
                       v
                  BATTERY + BMS
                       |
                       v
                LOCAL CONTROLLER
                       |
                       v
                   INVERTER
                       |
                       v
              COMMON MICROGRID BUS
                /      |                      /       |                      v        v         v
        Prosumer    Consumer    EV / V2G
           Node       Loads       System
              \        |         /
               \       |        /
                +------|-------+
                       |
                     GRID

A prosumer can generate and consume energy, while a consumer primarilyrepresents a load. A prosumer with surplus generation can make energyavailable to other nodes through the common electrical network.

SOC-Based Energy Management

Battery State of Charge is one of the primary decision variables in thesystem.

The controller continuously evaluates:

Battery SOC

Renewable generation

Load demand

Available battery energy

Charging/discharging condition

Grid availability

A simplified operating strategy is:

                    Start
                      |
              Read local inputs
                      |
          +-----------+-----------+
          |                       |
       SOC high                 SOC low
          |                       |
     Limit charging          Support load /
          |                  discharge if allowed
          +-----------+-----------+
                      |
              Check generation
                      |
          +-----------+-----------+
          |                       |
     Generation > Load       Generation < Load
          |                       |
      Store / Share           Battery / Grid
          |                       |
          +-----------+-----------+
                      |
                 Repeat cycle

The exact control thresholds can be configured according to the batteryand operating requirements.

Autonomous Switching Prototype

A working hardware prototype has already been developed using:

Arduino

Relay module

Battery

Electrical load

Power-source inputs

Automatic switching logic

The prototype automatically changes the power path according to theprogrammed operating conditions.

Prototype Concept

             Battery / Source
                    |
                    v
                 Relay
                    |
          +---------+---------+
          |                   |
          v                   v
       Load 1              Load 2

The Arduino monitors the defined input conditions and controls the relayto automatically select the appropriate supply path.

This prototype provides the hardware-level foundation for the largerautonomous energy-management architecture.

Peer-to-Peer Energy Sharing

The project extends local energy management toward P2P energy sharing.

For example:

     Prosumer 1                         Consumer 1
   Surplus Energy                       Energy Demand
         |                                   |
         v                                   v
     Local Node                         Local Node
         |                                   |
         +------------- COMMON BUS ----------+
                         |
                  Energy Transfer

If one node has surplus renewable energy while another node has adeficit, the architecture allows the available energy to be directedthrough the shared electrical network.

The objective is to move from a purely centralized energy-routingapproach toward distributed node-level decision making.

Droop-Based Coordination

The project investigates inverter-based droop coordination as amechanism for autonomous power sharing.

The basic concept is:

          Inverter 1
              |
            Droop
              |
              +--------+
                       |
                   COMMON BUS
                       |
              +--------+
              |
            Droop
              |
          Inverter 2

Each connected inverter responds according to its local controlcharacteristic.

Instead of requiring a digital command for every power transaction, theelectrical operating condition of the common bus provides the physicalcoupling between the participating nodes.

The droop-control architecture is a development objective of the projectand is being investigated through simulation and subsequent hardwarevalidation.

Bidirectional V2G

Electric vehicles are treated as additional distributed energy-storageresources.

A bidirectional charger can support two-way energy flow:

                 EV
                  |
          Bidirectional
             Converter
                  |
                  v
            Microgrid Bus

        Grid/Microgrid ---> EV
        EV --------------> Grid/Microgrid

Charging Mode

The EV absorbs energy from the microgrid when charging is required.

V2G Mode

The EV can supply stored energy back to the microgrid when the operatingconditions permit.

This provides additional flexibility for energy management andpeak-demand support.

Simulation Platform

The project includes a detailed MATLAB/Simulink/Simscape model of thehybrid microgrid.

The simulation work includes:

Solar PV generation

Wind generation

Battery energy storage

DC/DC power conversion

Inverter systems

PWM control

PLL synchronization

Three-phase loads

Grid interaction

Breakers

Fault modelling

SOC-based energy management

Consumer-side energy management

EVCS/V2G infrastructure

Measurement and data logging

The model provides the simulation foundation for studying the behaviourof multiple distributed energy nodes before expanding the hardwareimplementation.

Hardware and Simulation Relationship

The project is being developed progressively:

        SIMULATION
            |
            v
   Control Strategy
            |
            v
    Arduino Prototype
            |
            v
 Automatic Switching
            |
            v
   Multi-Node Prototype
            |
            v
  Advanced P2P + V2G
            |
            v
 Autonomous Hybrid
 Microgrid Demonstrator

The existing Arduino-relay-battery-load prototype demonstrates theautomatic switching portion of the system.

The larger research direction is to extend this foundation towardmulti-node SOC-based energy management, P2P energy sharing, inverterdroop coordination, and V2G.

Main Components

Renewable Energy

Solar PV

Wind generation

MPPT controller

Energy Storage

Battery

Battery Management System (BMS)

SOC monitoring

Control

Arduino prototype controller

Local control logic

PLC-based industrial control as a future implementation

Inverter control

Droop control

Switching and Protection

Relay modules

Contactors

Circuit protection

Fault detection

V2G

Bidirectional power converter

EV battery

EV charging/discharging control

Simulation

MATLAB

Simulink

Simscape Electrical

Key Operating Scenarios

Scenario 1 --- Renewable Surplus

Renewable Generation > Load
          |
          +--> Local Load
          |
          +--> Battery Charging
          |
          +--> P2P Energy Sharing

Scenario 2 --- Renewable Deficit

Renewable Generation < Load
          |
          +--> Battery Discharge
          |
          +--> P2P Energy Import
          |
          +--> Grid Support

Scenario 3 --- Low Battery SOC

SOC below operating limit
          |
          v
Limit / Stop Battery Discharge
          |
          +--> Grid Support
          |
          +--> Available P2P Support

Scenario 4 --- EV Available

EV Connected
     |
     +--> Charge
     |
     +--> Standby
     |
     +--> V2G Discharge

Key Performance Indicators

The project can be evaluated using:

Bus voltage stability

Power-sharing accuracy

Response time

Battery SOC behaviour

Renewable-energy utilization

Energy exchanged between nodes

Automatic switching response

Battery protection response

V2G charging/discharging performance

Grid dependency

Current Project Status

Completed

Five-node hybrid microgrid simulation foundation

PV and wind generation modelling

Battery and SOC-based energy-management logic

Consumer/load-side modelling

EVCS/V2G simulation infrastructure

Fault and protection modelling

Arduino-based automatic switching prototype

Relay-controlled battery and load switching prototype

In Progress

Decentralized P2P energy-sharing control

Droop-based inverter coordination

Multi-node hardware validation

V2G hardware implementation

Industrial PLC/BMS integration

Future Development

The planned development path is:

Refine the existing SOC-based control strategy

Validate autonomous switching under different load and generationconditions

Implement decentralized P2P energy-sharing logic

Validate inverter droop coordination in simulation

Expand the hardware prototype to multiple energy nodes

Integrate bidirectional V2G hardware

Implement industrial BMS and PLC-based local control

Validate the complete autonomous hybrid microgrid experimentally

Research Question

Can multiple distributed energy resources coordinate energygeneration, storage, consumption and exchange through local SOC-awarecontrol and electrical coupling, while maintaining reliable operationwithout requiring centralized control for every energy transaction?

Repository Structure

/
├── README.md
│
├── Simulink/
│   ├── Models/
│   ├── Subsystems/
│   └── Results/
│
├── Arduino/
│   ├── Source/
│   ├── Relay_Control/
│   └── Prototype/
│
├── Control/
│   ├── SOC_Management/
│   ├── MPPT/
│   ├── Droop_Control/
│   ├── P2P_Energy_Sharing/
│   └── V2G/
│
├── Hardware/
│   ├── Circuit_Diagrams/
│   ├── Wiring/
│   └── BOM/
│
└── Documentation/
    ├── Architecture/
    ├── Test_Results/
    └── Research/

Project Focus

Hybrid Microgrids • Renewable Energy • Battery Energy Storage •SOC-Based Energy Management • Autonomous Switching • P2P Energy Sharing• Droop Control • V2G • Distributed Energy Resources
