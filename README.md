# ReFound Terrestrial Vehicle

This was a project I've been meaning to do for a while and is inspired by the Tyco Rebound ars from the late 90's. (Link for reference https://tycocollectors.com/models/1996-tyco-rebound-4x4/)

<img width="600" height="470" alt="image" src="https://github.com/user-attachments/assets/c0bf8919-a4a9-4abc-97b7-473e31f42cdd" />

In essence I'm trying to make a redesign of thie vehicle with some modernizations for niche features and making a true "Rock Crawler Vehicle". Some for stretching my skills in protocol writing and motor controller design and others just for the fun and curiousity of it. Specifications are still to be written but some of the features im targetting are the following: 

Hardware Features: 
- Using STM32 w/ STM32U301R8 micro (convenicence since this is the micro that's used in my launchpad)
- Status Indicator Lights for Run State (Idle, Sentry, Run, Brake, Fault)
- Low Side Current Sensing (Differential Opamp)
- More to follow

<img width="1827" height="1218" alt="image" src="https://github.com/user-attachments/assets/7a78771e-a1f3-4667-be9f-305436f66a94" />

Software Features: 
- Running FOC based code. Some works has been done for arduino based designs (see https://docs.simplefoc.com/code) but going to use as inspiration rather than importing into STM code. See https://www.ti.com/lit/ml/slyp711/slyp711.pdf for explanation on to FOC vs Trap
- Live CAN FD Data feed from sensor data (List of sensors to develop. Transmit to website/server.
- Conservative fault values from sensor/health data (i.e. overcurrent, overtemp, humidity, overspeed, i2t, etc.)
- Audio ques for different run states

Mechanical Construction (Not my forte)
- First wave with 3d printered prototype parts
- Suspension, shocks, overall construction will be established the farther along this project gets. 

For Fun Features: 
- Terrain mapping from IMU data on each individual wheel.
- Regenerative braking per wheel
- More to follow

TODO: 
- Write Initial specifications
- Determine Timeline
- Get overall schemtic laid out
