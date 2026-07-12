# ReFound Terrestrial Vehicle

This was a project I've been meaning to do for a while and is inspired by the Tyco Rebound ars from the late 90's. (Link for reference https://tycocollectors.com/models/1996-tyco-rebound-4x4/)

<img width="600" height="470" alt="image" src="https://github.com/user-attachments/assets/c0bf8919-a4a9-4abc-97b7-473e31f42cdd" />

In essence I'm trying to make a redesign of thie vehicle with some modernizations for niche features and making a true "Rock Crawler Vehicle". Some for stretching my skills in protocol writing and motor controller design and others just for the fun and curiousity of it. Specifications are still to be written but some of the features im targetting are the following: 

On-Board Hardware Features: 
- Power Supply
    - 6s Lipo Batterys x2 Paralleled: https://us.ovonicshop.com/products/ovonic-5200mah-6s-100c-lipo-xt90?variant=49496336728344&currency=USD&country=US
    - Regulated Power Supply w/ Parallel Lipo Batteries --> Step down to Gate Driver Voltage --> Step down to 3.3v MCU
    - Custom dual battery pack management w/ protections (TBD)
    - Onboard FAN towards MCU and Power Management
- Micro
    - Using STM32 w/ STM32U301R8 micro (convenicence since this is the micro that's used in my launchpad and has CAN             support)
- Inverter Design
     - 4-Stack ESC/Motor Controller per Tire w intergrated IMus for level tracking
     - Low Side Current Sensing (Differential Opamp)
- 4-Layer PCB Desisgn

<img width="1827" height="1218" alt="image" src="https://github.com/user-attachments/assets/7a78771e-a1f3-4667-be9f-305436f66a94" />

Software Features: 
- Control Method:
     - Running FOC based code. Some works has been done for arduino based designs (see https://docs.simplefoc.com/code)           but going to use as inspiration rather than importing into STM code. ST has a decent starter guide for FOC                 implementation here: https://www.st.com/en/embedded-software/x-cube-mcsdk.html#overview.
     - FOC vs. trap selected for adutomatic torque adjustment for commanded RPM stability barring extreme load cases              (stall and locked rotor)
     - Smooth startup eliminating issues at lower rpm values
  
<img width="1919" height="1031" alt="image" src="https://github.com/user-attachments/assets/14d60fc2-151d-415a-8a43-780cc55afb12" />

- Safety Features:
      - Status Indicator Lights for Run State (Idle, Sentry, Run, Brake, Fault, Out of Range)
      - Conservative fault values from sensor/health data (i.e. overcurrent, overtemp, humidity, overspeed, i2t, etc.)
      - Audio ques for different run states
- Data Collection:
      - Live CAN FD Data feed from sensor data (List of sensors to develop. Transmit to website/server.


There's some pretty exciting projects already out there for simulation for FOC based motor controller design and tuning. Especially with markisus (check out his github page) https://github.com/markisus/motor_sim. It's a bit older but trying to find a good medium between this and MATLAB (Although if it gets too difficult to or outdated I won't get into too much of the weeds and sim with SimuLink) 

Mechanical Construction (Not my forte)
- First wave with 3d printered prototype parts
- Suspension, shocks, overall construction will be established the farther along this project gets.

Harnessing: 
- 18 AWG Silicon Wire (22 Max Amps)
- Braided Looms: https://theruckshop.com/product/split-braided-wire-loom-clean-cut-1-2-or-3-4-inch/

For Fun Features: 
- Terrain mapping from IMU data on each individual wheel.
- Regenerative braking per wheel
- Waterproof enclosure designs:
      - I've previously encased wire harness with silicone, encased, heat shrunk, wrapped with electrical tape, then
        encased in liquid electrical tape for ROV design. There's been some suggestions here                                       https://www.instructables.com/How-to-Waterproof-Your-Electronics-or-PCBs/ but want to find a good industrial               solution for the final design. Typical RC cars are limited to IPX4 ratings, so I'll shoot for that standard.
- Dedicated Cloud based app & tracking
      - Aggregate data for collected sensor data and fault conditions when the car is farther and out of range.
- Path Return
      - Remembers the track path and distance it went on, as long as there was no fault condition en route from change
        from IDLE to RUN, it can take over the wheel and return back to the user when it gets out of range of controller
        transceiver.

TODO: 
- Write Initial specifications
- Determine Timeline
- Get overall schemtic laid out
