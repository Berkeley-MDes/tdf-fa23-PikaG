# Weekly Report 15 - 11/30/2023 - 12/7/2023

## Summary

## Final Project Report
### Final Project Showcase
**Presentation video link:** https://youtu.be/Mqj_ka-ls20?si=v70H1NQr5XaOG3qm
<img width="975" alt="截屏2023-12-07 18 48 35" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/39aee646-e729-4611-b705-df16021bcc77">
<img width="972" alt="截屏2023-12-07 18 48 17" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/d2df3269-8dcb-491d-9d4c-743f0f191119">

### Project Background
The concept of Origarden originated from a vision to bridge the gap between indoor human activities and the natural world. In modern society, where our majority of time is spent indoors, opportunities for direct interaction with nature have significantly diminished. The Origarden project was meant to bring the beautiful dynamics of outdoor plants into indoor spaces, building a connection with nature for the users.

### Project Description
Origarden consists of two main components. The first is a sensor kit designed to gather essential data for plant growth, such as soil moisture and sunlight. The second component is an installation with origami flowers to replicate the dynamics of real plants and OLED displays to showcase the collected data.

### Design & Fabrication
The design and fabrication process have the following three main parts:
**Design & Fabrication of Origami Flowers**
We utilized the Grasshopper plugin "Crane" for our design. Within our Grasshopper program, the key component is the Crane solver, which serves as the core computational unit. Initially, we defined the positions of key points that constitute the form and specified the boundaries and folding lines. Subsequently, we defined the number of petals by specifying the angles of the flower's petals. Ultimately, the Crane solver was employed to observe the folding configuration of the flower.
During the design research process, in conjunction with our hardware device, we altered the angles between the petal positioning lines, simplifying the flower from eight petals to four. Simultaneously, by adjusting the parameters of other positioning points, we modified the morphology of the petals. We compared these two approaches and selected our final petal design.

**Design & Fabrication of Mechanism**
The mechanism's design was the challenge for our project. We designed the structures for using the servo motors to control the unfolding of the origami flowers. We used 3D printing to fabricate the structure. In this step, we experienced several iterations to make sure that the mechanism worked seamlessly with the origami flowers.

**Software Control**
We use Photon2 devices, the system transmits data collected by sensors via the Particle cloud. The code controls the servo motors based on the received data, ensuring that the origami flowers' movements are synchronized with the outdoor plants. 

### User Scenario
Origarden can be set up in various indoor environments, such as homes and offices. You can take the sensor kit with you when exploring nature. Simply place this device next to a plant that interests you. When you return indoors, you can then observe essential information about that specific plant and have interaction with the corresponding origami representation.

## Conclusion & Speculation
