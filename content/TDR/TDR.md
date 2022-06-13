---
abstract: |
  The Lehigh University Underwater Robotics Team began work in summer of
  2021. In our first year of competition, we strive to lay the
  groundwork for competitions in the future years and research acoustic
  signal processing, underwater visual simultaneous localization and
  mapping (SLAM), and a comparative study on multi-channel PWM drivers.
  Four sub-teams--*mechanical, electrical, software,* and
  *business*--work together to design and manufacture the autonomous
  underwater vehicle (AUV), named Osprey, at Lehigh Underwater Robotics.
  Each team takes on a number of tasks and communicates and collaborates
  together to produce the final product. The electrical team provides
  the computer and hardware as well as the power supply that the
  mechanical team uses for the drone's thrusters and other components.
  The software team programs the robot to perform the competition tasks
  autonomously. The business team focuses on documentation and
  organization of funds.
author:
- Mikael Asfaw, Junchen Bao, Heidrun Cobb, Zemichael Gebeyehu, Logan
  Kramer, Andrew Langenau, Sophia Martino, Junan Mei, Adam Mekay, Daniel
  O'Keeffe, Hanqing Qi, Layne Raczy, Olivia Reed, Fengyi Sun, Lily
  Swider, Xinhao Tang, Nathaniel Todd-Long, Heling Wang, Fangzheng Yu,
  Rosa Zheng
bibliography:
- references.bib
date: June 12, 2022
title: |
  Lehigh University RoboSub Technical Design Report\
---

# Competition Strategy

## Team Makeup and workflow

The team is made up of four subteams: *mechanical, electrical, software*
and *business*. Each team is responsible for designing certain
components of the drone and collaborating so that each element fits
together accurately.

As a team, overarching goals are set, outlined by the RoboSub
requirements. There is a general team leader and four sub-team leaders
who are responsible for administration and defining and enforcing
sub-goals. These sub-goals are defined in order to achieve the larger
goal by breaking it up into smaller tasks; they get accomplished on a
daily or weekly basis, and build upon themselves to accomplish the
larger goals.

## Software Strategy

The main task of the software sub-team is to build on the work of the
mechanical and electrical sub-teams and integrate all the results to run
smoothly. In this process, we use several different methods to
collaborate and achieve the results we require. These methods include
training models for image recognition using YOLO [@yolov3], real-time
image processing, use of models in OpenCV, programming in Python (and
then using C++ to improve efficiency later), and control of AUVs using
ROS and MavROS.

## Mechanical Strategy

*Team communication* Due to part of our team being virtual we had to
find a way to effectively communicate with the whole team. We solved
this issue by having those who could be in-person meet up everyday to
work, and those that were virtual work remotely while having the whole
team communicate ideas over Slack (a collaborative team app), thus
allowing all members of the team to remain included and work together
effectively. *Settling on Designs* Often when our team was designing a
component for the chassis we'd come up with multiple viable designs. The
team would come together to discuss the pros and cons of each design and
reach a consensus on which solution works the best.

## Electrical Strategy

The electrical sub-team has the essential job of supplying our drone
with power and ensuring that all of the components will be powered and
operate when instructed to. The software and mechanical team are both
reliant on the electronics to power the thrusters as well as the sensors
that provide crucial localization information. This is the first time
the Lehigh Underwater Robotics team will be competing in the RoboSub
competition, so our first challenge is to design a power distribution
schematic to supply an adequate amount of power to all of the AUV's
components. Our electrical team used the BlueROV2, created by
BlueRobotics [@BlueRobotics], as inspiration to help guide the basis of
our design. There were modifications that our team had to make in order
to incorporate additional components not found in the BlueROV2 (Pixhawk
4, NVIDIA jetson, additional cameras, a gripper, etc).

## Business Strategy

The business team works closely with the three other teams to understand
what their tasks and contributions are. They contribute to compiling the
documentation in the TDR, the team video, and weekly team update.
Additionally, our team works with outreach in getting interest from new
members and potential sponsers.

# Vehicle Design

## Mechanical

[Mechanical design for underwater drone.]{.image}

### Frame

Marine grade plastic and carbon fiber nanotube are used for plates and
connectors, respectively. These materials are lightweight alternatives
to aluminum or other metals without compromising structural integrity.

One of the main considerations taken into account while designing the
frame was the distribution of weight and buoyant forces. Specifically,
the battery enclosures are positioned at the bottom of the frame and the
main enclosure is positioned towards the top of the frame, between the
two battery enclosures. This detail, as seen in Figure
[1](#mechdes){reference-type="ref" reference="mechdes"} allows the
design to have a stable equilibrium when in the upright position due to
the net downward force of the batteries and the net upward force of the
main enclosure while underwater. These forces were calculated using the
volume of air in the enclosure compared to the weight of the components
inside.

[Electrical Schematic for underwater drone.]{.image}

### Thrusters

*Positioning:* We wanted to maximize forward and backward movement speed
while also having the robot remain maneuverable with many degrees of
freedom. We used the same thruster layout from the BlueROV2 because we
had already developed software in Summer 2021 compatible for controlling
the thrusters. The team did not yet consider the benefits and
disadvantages of another layout and did not have access to a simulation
showing the advantages and disadvantages of other thruster layouts.
*Mounting:* A major concern of ours was how to mount the thrusters to
match the correct positining while also making sure it would retain its
structural integrity, remain intact, and remain balanced in the event
that the robot hit an object while moving underwater. This was
especially important for the top, angled thruster mounts. The angling on
the thrusters cause the mounts to lose structural integrity, and the
thrusters and mounts stick out from the main body of the chassis which
makes them more fragile.

### Torpedo Launcher

The goal in designing a torpedo launcher was to keep it as simple as
possible. Our design relies on one servo with a gear that moves a linear
actuator allowing for a torpedo to be released from the housing. The
torpedo is propelled by a spring that is held under tension by the
torpedo and the linear actuator. A notch all the way around the radius
of the torpedo allows the torpedo to fit into the flat length of the
linear actuator and hold the spring down, creating positive potential
energy in the system. When the servo translationally moves the linear
actuator to one side, the torpedo is released from tension and the
spring propels it forward into the required space for scoring points.

## Electrical

### Design Obstacles

One of the major design obstacles the electrical team faced was
installing the entire hardware system inside of a water-tight acrylic
tube. The electrical team collaborated with the mechanical team to
design and print a harness that would safely secure all of the AUV's
hardware.

The electrical team also works closely with the software team to select
the best sensors to implement into the AUV. This collaboration is
critical since the selection and wiring of sensors is what will provide
the software with sufficient data to successfully navigate through the
tasks.

### Battery

Our drone is powered by two lithium-ion batteries connected in parallel
(supplying 14.8V). The electrical team decided to use a low voltage
disconnect module, switching between batteries when the battery dropped
to a certain level, to protect the batteries from discharging too much
and causing permanent damage.

Then, a few UBECs (V-V converter) are implemented to supply the desired
voltage (5V) to power the Pixhawk 4 [@5980229]. The voltages are
distributed via terminal boards and power the whole system. We are using
the Pixhawk 4 as our AUV's flight controller. The flight controller
controls all 8 thrusters, the leak sensor, and the pressure/depth sensor
and communicates this data into the Nvidia jetson. The Jetson (central
processing unit) would then analyze these data along with the data
obtained from the three cameras connected directly to the Jetson. The
schematic is seen in Figure [2](#schematic){reference-type="ref"
reference="schematic"}.

## Software

We will mainly use ROS2 [@doi:10.1126/scirobotics.abm6074],
YOLO [@yolov3], and OpenCV [@opencv_library]. Robot Operating System 2
(ROS2) is an open-source software development kit for robotics
applications. Using it can help us save time on integrating different
robot functions. You Only Look Once (YOLO) is a real-time object
detection algorithm. Using YOLO is easy to train with the custom data
set, which can be an excellent way to recognize the image in the
different tasks. OpenCV is an open-source computer version platform
library and using it can provide a good way to use the drone in a little
to no data training situation.

### Image recognition

OpenCV [@opencv_library] is an open-source code, and using it can help
reduce a lot of processing power compared to the other machine learning
platforms, and we can do the edge detection for the gate and help us
find and locate the position of the gate buoys with ease. The grayscale
and color isolation make it easy to locate the gate. We use YOLO to
train a custom model for the image on the gate and the buoys in the
task. YOLO is a solid open-source neural network code that can use
limited data to get a good image recognition result. Therefore we do not
need to collect tons of data. We can still get a good result by just
using a small number of pictures collected from the drone.

### Motion Control

MAVLink [@8743355] is a lightweight messaging protocol for communicating
with drones. This provides an easy way to communicate with the different
parts of the drone and send control signals, with thrusters, the
battery, and different sensors. MavROS is a ROS package that enables
MAVLink communication between computers using ROS.

# Experimental Results

## Pool Tests of BlueROV2

Testing has been done over the past six months in one of the pools on
our University's campus. We used the BlueRobotics BlueROV2 for most of
our testing, where we recorded video and tested Python scripts on its
Raspberry Pi. As we moved to our own design, we test scripts in ROS or
Python on the Nvidia Jetson. The video footage was collected for
training our models for autonomy.

In addition to the BlueROV2 which has a Raspberry Pi, we designed an
enclosure containing the Nvidia Jetson and a camera for testing that is
more like the new design, as the camera is the same. This device does
not include thrusters, so instead a member swimming in the pool guides
it manually. We used a script to record the video, where it waits a
certain amount of time to start recording as we get the device ready for
the water, then records for a set amount of time. Then, we download the
file using SSH file transfer protocol (SFTP) or secure copy (SCP). This
video is used for training the model, and the design of the enclosure
provides the same footage that Osprey would see.

## Bouyancy Testing of Carbon Fiber Frame

The new design has a different structure than the BlueROV2 we used for
testing; therefore, it has different balance and buoyancy. We needed to
calculate the buoyancy so it is positively buoyant as required, but we
did not have an estimate on how it would behave in the pool. So the team
placed it in a tub to feel how it is balanced and where buoyancy foam or
weights may need to be placed.

# Acknowledgements {#acknowledgements .unnumbered}

We would like to thank the people who supported this project over the
past year. Specifically, we acknowledge Lehigh University's ECE
department; we thank Professor Rosa Zheng's guidance and inspiration to
the students on our team; and we thank Bill Maroun for technical design
guidance.

We would also like to thank our donors from crowdfunding, who helped
make our drone possible. Finally we thank Lehigh's Mountaintop Program
for providing the groundwork and funding on our team project.

::: {.center}
::: {.tabular}
p2cm p2cm p3.5cm p2cm p2cm p1cm p2cm *Appendix A* **Component** &
**Vendor** & **Model/Type** & **Specs** & **Custom/ Purchased** &
**Cost** & **YOP**

Battery Check (2) & BlueRobotics & BATTERY-CELL-CHECKER-R1 & 2-6s Li-Ion
Battery & Purchased & \$30 & 2020

Cable Plugs (16) & BlueRobotics & PENETRATOR-BLANK-VP & M10 Threads &
Purchased & \$64 & 2020

Battery Cables (2) & BlueRobotics & BROV2-CAB-POWER-SET-R1-RP & 5.5mm &
Purchased & \$136 & 2021

I2C Converter (1) & BlueRobotics & LEVEL CONVERTER-R1-RP & 3.3V &
Purchased & \$20 & 2020

Watertight Enclosure (1) & BlueRobotics & WTE6-ASM-R1-VP & 6\" Series &
Purchased & \$337 & 2021

Dual Row Terminal Strip(1) & GUBCUB & GUB-JXDZ & 10.0 A & Purchased &
\$6.99 & 2021

Voltage Disconnect Module (1) & CZH-LABS & MD-D1021V3 Series & 12V/30A &
Purchased & \$25 & 2022

Rechargeable Li-Ion Battery (2)

Orange Plastic Sheet (2) & BuyPlastic & PLA-000018-020 & 11.75\" x
23.75\" & Purchased & \$21.46 & 2022

Dropper Brushless Servo(1) & Traxxas & e-revo Slash T-maxx Summit 3908 &
6 V & Purchased & \$39.95 & 2021

Camera & ELP Sony & IMX322/323 & 100° FOV & Purchased & \$63.99 & 2022

Camera & ELP Sony & IMX322/323 & 170° FOV & Purchased & \$62.99 & 2022

Plastic Sheet (2) & ePlastics & SEABOARDBLK-0.500TEX54X48 & 1\" X 54\" X
48\" & Purchased & \$268.26 & 2022

Watertight Enclosure (2) & BlueRobotics & WTE3-P-TUBE-8P75-R1-RP & 3\"
Series & Purchased & \$262 & 2022

SOS Leak Sensor & BlueRobotics & SOS-SET-R1-RP & 3.3-5V, 20mA &
Purchased & \$32 & 2021
:::

::: {.tabular}
p2.2cm p2cm p3.5cm p2cm p2cm p1cm p2cm **Component** & **Vendor** &
**Model/Type** & **Specs** & **Custom/ Purchased** & **Cost** & **YOP**

Pressure/Depth Sensor & BlueRobotics & BAR30-SENSOR-R2-RP & 30 Bar
(300m) & Purchased & \$85.00 & 2021

Ping Sonar & BlueRobotics & PING-SONAR-R3-RP & 30° Beam width, 300m &
Purchased & \$360 & 2021

Pixhawk 4 & HolyBro & & & Purchased & \$190 & 2020

Thrusters (8) & BlueRobotics & T200-THRUSTER-BROV2-CCW-SPARE-R2-RP & &
Purchased & \$1,680 & 2020

Nvidia jetson Developer Kit & NVIDEA & Nano & 4GB & Purchased & \$99 &
2020

ESC(8) & BlueRobotics & BESC30-R3 & 7-26V & Purchased & \$288 & 2022

Circuit Breaker & Bumbesti & HBD-CXFH-15A-2P & 15A & Purchased & \$19.99
& 2022

Diodes (2) & Onsemi & MBR40250TGOS-ND
:::
:::
