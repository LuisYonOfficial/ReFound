# ReFound Terrestrial Vehicle

This was a project I've been meaning to do for a while and came about while hiking in the Tetons in Wyoming and further encouraged by some fun afterwork RC development between colleagues at my company. I've messed with RC cars in the past and although they're pretty speedy, i'm more interested in developing a variant of it that is more attuned to a high degree of torque control with respect to an extremely varied terrain mapping (almost like a tank in terms of mobilty. Something that could survive high altitude climbs and hold brakes at high degree inclines. Something that if I dropped down in a quarry would be able to manuever around great with FPV control and sensory feedback. On a more practical note I could slot my phone on the headpiece of the vehicle for some wildlife photos with a more grounded view vs your typical drone photography or cool positions for astrophotography.

<img width="1195" height="541" alt="image" src="https://github.com/user-attachments/assets/9ab773d5-8f91-4d7e-83ce-70b0d638f7c2" />

The mechanical design I envision is along the line of a Tyco Rebound ars from the late 90's. (Link for reference https://tycocollectors.com/models/1996-tyco-rebound-4x4/)
<img width="600" height="470" alt="image" src="https://github.com/user-attachments/assets/c0bf8919-a4a9-4abc-97b7-473e31f42cdd" /> 

Some for stretching my skills in protocol writing and motor controller design and others just for the fun and curiousity of it. Specifications are still to be written but some of the features im targetting are the following: 

Motor Selection: 
- After preusing online, without going too extreme in terms of price I've settled on theQuiCRUN Fusion SE Motor.
    - Datasheet: (https://cdn.shopify.com/s/files/1/0109/9702/files/User_manual_XERUN_AXE_R3_system.pdf?v=1716074509)

On-Board Hardware Features: 
- Power Supply
    - 6s Lipo Batterys x2 Paralleled (Still setting power levels but something like https://us.ovonicshop.com/products/ovonic-5200mah-6s-100c-lipo-xt90?variant=49496336728344&currency=USD&country=US in mind)
    - Regulated Power Supply w/ Parallel Lipo Batteries --> Step down to Gate Driver Voltage --> Step down to MCU Voltage
    - Custom dual battery pack management w/ protections (TBD)
    - Onboard FAN towards MCU and Power Management
- Micro
    - Using STM32 w/ STM32F042K6 micro (Industry favorite, and easy to source for testing https://estore.st.com/en/nucleo-f042k6-cpn.html?ecmp=tt48069_gl_ps_feb2026&aw_pl=&aw_c=22473118548&aw_de=c&aw_dm=&aw_tg=pla-2443119483834&aw_gclid=CjwKCAjwmdLSBhANEiwAkREMNz5DVm-KAH9L_AlRRRa18S1szPnDuzbXzbn8Uvmyu7ACAvqGHG1wvBoCgxYQAvD_BwE )
- Inverter Design
     - 2-Stack ESC/Motor Controller per rotating axle (4WD)
     - Low Side Current Sensing (Differential Opamp)
- 4-Layer PCB Desisgn

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
<img width="265" height="300" alt="image" src="https://github.com/user-attachments/assets/322f637b-2ee8-40cc-8d59-b49d76de5187" />

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
- Retractable arm for grabbing materials or a lost item from a hike.

TODO: 
- Write Initial specifications
- Determine Timeline
- Get overall schemtic laid out
