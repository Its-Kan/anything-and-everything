[[Dylan Soco - Final Report Marksheet Y1.pdf]]
[[WEEK+13+FINAL+REPORT.pdf]]
```table-of-contents
```
# Product Concept (10%)
> [!NOTE] Description
> main aim, who it's targeted at, marketing ideas
## Product Aims
Our company, Dipole Electronics, was conceived with one main goal in mind: **to unite old and new music technologies**. We looked for inspiration in history: from early electronic instruments like a theremin, to traditional instruments like violins. However, we wanted our product to showcase the rich history of music technology, so we looked further back for more archaic and niche instruments that we could add a modern electronic twist. 10, 11, 13, 16, 18, 19


[^1]: guiltyx

After this consideration, we discovered the hurdy-gurdy, a mechanical violin-like instrument that was popular in the 13th century. We loved the extra dimension of expression the crank was able to provide, as well as the rich history behind it. When also seeing the lack of "rate of change" controls in modern synthesisers, we decided to make an electronic hurdy-gurdy, called the **The WindUp**.
## Marketing
With learning on the forefront of our product concept, we will be marketing towards educational institutions. We hope to target multiple stages of education, with our plans on marketing The WindUp. We will be offering three kits, whose amount of self-assembly increases based on the level.
- The first level will be shipped **fully assembled**, aimed towards younger students in primary school. This level will focus on sound production, where students can learn about different waveforms and their sounds, as well as creating their own.
- The second level will be **flat-packed and comes disassembled** with instructions, aimed towards older students in secondary school. This level will focus on electronics assembly, where students can learn about soldering and circuit organisation.
- The third level will be shipped with **just the electronics** and 3D model files, aimed towards engineering students. This level will focus on manufacturing, where students can learn about laser cutting and 3D printing.
![[MusTech Project 2 FINAL REPORT marketing.png]]
# Description of Entire System (10%)
> [!NOTE] Description
> technical overview, specification, use of audio synthesis
## Usage
To start playing The WindUp, the device will need to be plugged into the mains power supply, as well as connecting the audio jack to a speaker system/amp. 

To play The WindUp, place the device button-side down onto your left or right thigh, with your left hand going over the key-box. and your right hand holding the crank (*see Figure 1*).  The keys are analogous to a keyboard, spanning two octaves ranging from C4 to B5, and the crank can be rotated clockwise, or counter-clockwise. To play a sound, both a key on the keyboard has to be pressed while the crank is rotating, where the keyboard dictates pitch, and the crank's speed dictates volume, and its positive acceleration dictates pitch bend.

Currently, we have 4 parameters on the WindUp, that can be controlled on the digital LCD screen, using the D-pad and back/select buttons. The parameters include:
- wave shape
- chorus
- reverb 
- filter
![[SittingPosture1.png]]
## Technical Overview
In terms of specification, see *Figure 2* for a parts list.

| **Hardware**   | **Specification**      |
| -------------- | ---------------------- |
| Microprocessor | STM32F407VG            |
| Board          | Discover Board         |
| LCD Screen     | 64x128 NHD12864WG-BTGH |
| Crank          | 12v DC motor           |
| Keys           | Blue Keyboard Switches |
| D-pad          | Pushbutton Switches    |
| Housing        | Acrylic & PLA          |
The housing is comprised of laser-cut 

The crank is made from a 12v DC motor, which 

The code runs locally on the microprocessor using C, and is powered through a 15V mains connection. There aren't any speakers on the instrument, so to hear audio, the audio jack must be connected to a speaker/amp. 

Sound generation and audio synthesis is handled on the microprocessor, and uses wavetables to generate sine, triangle, sawtooth and square waves locally. Using the digital sound management system, crank and keyboard allows the user to modify the wavetable's frequency, timbre and amplitude.

![[Flowchart.png]]
# Analysis of Effectiveness & Future Plans (10%)
> [!NOTE] Description
> achievements of the prototype compared to the specification in the initial report, quality of sound and user interfacing, further work needed as a group to complete the product prototype
## Analysis of Effectiveness
We fulfilled the main ideas and ambitions laid out in our specification with our prototype (*see Figure X*). We were able to create a product that resembles a traditional hurdy gurdy, while integrating modern synthesiser elements with the unique controls. 

|              | **Spec Point**                                                                                       | **Met?**                       |
| ------------ | ---------------------------------------------------------------------------------------------------- | ------------------------------ |
| **Hardware** | All circuit boards and components should be connected using removable sockets.                       | ✅                              |
|              | A 6mm and 3.5mm audio jack should be present for use with headphones and recording.                  | ✅                              |
|              | The wind-up will be battery and USB powered or wall-wart powered depending on the operating voltage. | ✅- Powered using wall-wart     |
|              | Mechanical keyboard buttons, switches, and potentiometers should be utilised                         | ✅                              |
|              | A 128*64-pixel graphical LCD should be used                                                          | ✅                              |
| **Software** | All audio generation must be performed on an STM32f4                                                 | ✅                              |
|              | Audio generation should be low latency                                                               | ❓- Not tested yet              |
|              | Menus/ the display should be easy to navigate                                                        | ❓- Not tested yet              |
|              | Code should be well documented with descriptions of how it works                                     | ✅                              |
|              | A range of unique sounds should be producible using the wind-up                                      | ➖ - Only tri, sqr, saw and sin |
| **Housing**  | The wind-up should resemble a traditional hurdy gurdy                                                | ✅                              |
|              | Sharp edges should be minimised                                                                      | ✅                              |
|              | Handle should rotate smoothly with some but not excessive resistance                                 | ✅                              |
|              | All electronics should be suitably protected                                                         | ❌                              |

The housing is likely the biggest achievement of our prototype. The clear parts of the housing are laser-cut acrylic, and the white plastic is 3D printed PLA. With how it's modelled, all the segments can be cut/printed flat, and assembled modularly, using screws to fasten all the components together. The initially complex procedure of creating the 3D model means we're able to fulfil our goal of allowing the product to be self-assembled. 

![[MusTech Project 2 FINAL REPORT product.png]]

We were able to successfully implement two sensors to detect user inputs: the crank and the keyboard, as well as the digital sound management system using the LCD screen. The multiple controls The WindUp has allows added layers of musical expression, and showcases the parameters that can be modified in audio synthesis. The digital 

In terms of the educational aspect of our product, our design allows our idea of multiple levels of shipping to reach a large range of students: 
- The fully built kit allows students to explore sound generation and production.
- The disassembled kit allows students to practise electronics assembly.
- The electronics only kit allows students to learn about product manufacturing and soldering.

In terms of price, as it's a structurally complex, novel model with a few unique components, the cost of components and manufacturing reflects this, with the fully assembled build costing around £57, however we can cut costs by buying in bulk. The selling price can have some variation with our multi-level marketing plan by cutting assembly and manufacturing costs, meaning further accessibility for schools and other educational institutions. Our product is drastically cheaper than similar products such as the DigiGurdy costing £698[^1] or the Nerdy Gurdy costing upwards of €320[^2], and so is perfect for educational institutions.

[^1]: “Order,” _Digigurdy.com_, 2024. https://digigurdy.com/services/
[^2]: “Hurdy Gurdy – Nerdy Gurdy,” _Nerdygurdy.nl_, 2025. https://www.nerdygurdy.nl/product-category/hurdy-gurdy/
## Future Plans
Our company has very ambitious plans for the future, outlined in our vision in our Tender Presentation Video. Although all of the requisite parts of the design has been completed, we haven't yet been able to arrange them all together. 

Looking to the future to expand our initial idea, our main focus would be implementing a drawable wavetable, which would be able to translate visual waveforms into sound, that can be further controlled using the controls and the parameters provided. This addition would allow The WindUp to explore sonification, and can teach the user a sense of how the shape of a waveform can shape its sound. 

We would also like to develop some material containing information that will educate about the history of the hurdy gurdy, while giving context on aspects of its design. We think learning about the history behind past music technologies is equally as important as developing and innovating future technologies, and our past-future hybrid instrument can be a great vehicle to bridge these new and old instruments.  

As for ideas reaching beyond our specification, we considered using a second microprocessor to solely handle the button matrix, as audio synthesis is a very computationally intensive task for a single microprocessor to handle. Currently it handles both, which might make the system have latency, or inconsistent. Adding another microprocessor would put less workload on the audio synthesis, and our controls would be more responsive.
# Individual Contribution (40%)
> [!NOTE] Description
> achievements of the prototype compared to the specification in the initial report, quality of sound and user interfacing, further work needed as a group to complete the product prototype
## Individual Role and List of Contributions
Using what we've learnt from the previous Music Tech Project, we as a group shared what we were strong at, and wanted to pursue more in this project. I wanted less of a managerial role while still being able to delegate tasks. With both my skills in coding and 3D art/graphic design, I was appointed the roles of Lead Programmer and 3D Artist/Graphic Designer. Below are my individual contributions for each role:
### Lead Programmer
- Set-up a GitHub repository  
- Wrote guides on how to use Git and GitHub in a professional context (*see Appendix X*)
- Created STM32 Makefiles to work in the STM environment
- Wrote algorithms and flow-charts outlining the internal functionality of the product
- Programmed the code for the menu system, button matrix logic and tuning calculations
### 3D Artist/Graphic Designer
- Recreated, refined and animated company logo.
- Created visual assets for company identity.
- Video edited, animated, sound-designed, and produced visuals for Tender Presentation Video, as well as contributing to voice-overs.
### Miscellaneous
- Set-up a Discord server for communication, store change logs and temporary file storage
## Technical Detail
My technical contributions can be seen in my programming contributions to the instrument. Before then, I set-up my coding workflow:
- **IDE**: Visual Studio Code
- **Language**: C
- **Repository**: GitHub

First, I figured out the logic for how the menu system must work, using flags. I used my code from the previous project, as it had many similar elements, however I needed to change it to work in C, as well as adapt it for our project. The algorithm for it looks like:
1. Detect when a D-pad button is pressed
2. Add 1 to the current variable flag. If it's outside the bounds, the value should wrap around.
3. Update the corresponding element in an array holding all of the parameters.
4. Translate the current element into a string.
5. Display the string.
6. Go back to 1.

To implement this, I defined multiple variable and array flags that tracks what variables have been changed, and will later be passed on to the sound generation function (*see Appendix X*). 
- `currentLayer` and `currentVariable` store counters for whenever the d-pad buttons are pressed.
- ``menuLocation`` wraps both `currentLayer` and `currentVariable`, and stores what layer the LCD screen should display (variables for top layer and values for the bottom layer), as well as what variable should appear on the bottom layer.
- `variableValue` stores 4 counters for each variable
- ``variableValueWrap`` wraps around ``variableValue``, and stores the values of each variable, to be passed to the sound generation function.

![[MusTech Project 2 FINAL REPORT flags.png]]

Using interrupts, the d-pad runs a function whenever it's pressed. Up and down switches the `layerSelect` between 1 and 0, using a simple NOT operator. The left and right buttons rely on the value of `menuLocation[1]`, which is checked using an if statement. As the variables have multiple states it could be, I had to implement wrapping to ensure the button counters translate into 4 unique values. I accomplished this by using the modulo operator on the absolute value of the counter, which allows the counter to cycle between 0, 1, 2 and 3. This would then be displayed on the LCD screen (*see Appendix X*).

![[MusTech Project 2 FINAL REPORT code 2.png]]

To save pins, a button matrix is used for the 25 keys on the keyboard. As of writing this report, the specific pinouts for the buttons haven't been defined yet, however I have written the logic for handling the button matrix and turning it into a frequency.

I translated the button matrix into an array, whose row and column corresponds 1:1 to the physical button matrix. Each element in the array holds a function, which calculates the corresponding frequency using the 12 equal temperament (12ET) tuning system (*see Appendix X*). The function calculates the note X semitones up from C4, based off A = 440Hz. I have also written functions for the Pythagorean and just intonations if we ever want to experiment with different tuning systems in the future.

![[MusTech Project 2 FINAL REPORT 12tert.png]]

For the LCD screen itself, I used example code provided by Newhaven Display to configure and render the text, accessed from Newhaven Display's official support website [^3]. This code initialised, and provided functions to display text on the LCD screen. I made a temporary function `displayLCD();` which I can replace with the drivers functions.  

[^3]:  “Example Code – Newhaven Display Support Centre,” Newhaven Display, 2025. https://support.newhavendisplay.com/hc/en-us/categories/4409527834135-Example-Code/ 

The code that handles the crank and sound synthesis weren't written by me, however I am responsible for putting all these component programs together in the top level program. As of writing this report, the pinout hasn't been completed yet, however the infrastructure for arranging all of the programs together has been established using header files. 

Once I have received the pinout in the future, I would be able to initialise all the button inputs. Two pins should register as an active-high signal, which should be translated into two integers from 0-4 based on their row/column. Their respective row/column would be passed on to the matrix, and then the frequency from this would be passed onto the audio synthesis code. 
# Reflective Analysis and Peer Review (20%)
> [!NOTE] Description
> Reflection on Group Roles, Project Management, Peer Review, Societal Impact (SEERS), Reflection on Individual Strengths
## Group Reflection
Our group roles remained very rigid throughout the project, and everyone in general stuck to their assigned roles (*see Figure X*). We were able to setup consistent weekly meetings, and if we had people call in absent for a meeting, we would organise a meeting on another day, usually online. This kept us accountable, as well as giving us a clear progression per week thanks to Alice. 
![[MusTech Project 2 FINAL REPORT roles.png]]
With how we divided the roles, our workload was spread somewhat evenly. Some people had more work than others, however none of the work solely depended on one person. However, our collective time management started to falter deeper in the project, as some members experienced personal difficulties that impacted their ability to contribute fully at certain stages of the project. We planned to make a roadmap for development, however unfortunately we weren't able to make one, which could've contributed to our time management issues.

In terms of communication, we used both WhatsApp and Discord, the former for temporary messaging and the latter for more permanent progress reports and notes. Discord proved to be effective to have more focused discussions on specific parts of the project, as we were able to create different channels for each section, as well as hold meetings if we weren't able to have a meeting in person (*see Appendix X*).

![[MusTech Project 2 FINAL REPORT discord.png]]

Unfortunately a similar issue arose from last year: as a lot of the software aspects depends on the hardware, so any testing of software had to wait until the hardware was completed, which made us push forward our personal deadlines. Our housing being structurally complex and modular, as well as waiting for our acrylic to get laser cut caused significant delays in our roadmap. Next time, we should re-prioritise our tasks, so we are able to work on more aspects of the project without depending on a specific person/task to be completed.

As mentioned previously, we weren't able to get a fully functioning prototype due to personal obstacles during development. In the future, it would be beneficial if we discussed any potential problems that might impact the development roadmap, and what we could do as a group to either support, or mitigate the consequences of someone needing a break.
### Personal Reflection
As for personal progress, I took lessons I learnt from the last project to be more efficient in this one. Although I wasn't managing the project, I was still able to use my leadership skills to delegate programming tasks, and coordinate everyone's work to ensure consistency. This lightened my workload, and enabled me to focus more on my own tasks. I had also discovered effective ways of maintaining my own personal time management with timeboxing and scheduling, so I was able to complete my tasks consistently and on time.

Since the last project, I've been able to be more organised to make the group's and my workflow more efficient. As the code was a more collaborative effort, I was able to learn about Git, repository management and version control to ensure everyone was able to work on the same code without version clashes. My written guides on the subject allowed everyone to name branches and submit pull requests using consistent industry-standard practise. I also added multiple comments to better explain my logic to the others, as well as using header files to segment everyone's code.

In future projects, I think emphasising the agency some tasks require in a Gantt chart or roadmap, to prevent delays in work. In some points during the development, I had some personal challenges that affected my work, however I was able to inform the group about it. To keep work moving consistently, I could've had some of my work shared with others so if I, or any of the other programmers, had to take a step back, the others could still pick up the work. I also tend to accept any changes without raising my voice enough, so next time, I would like to be more vocal about any ideas that might not be plausible, or if we need to scale back things a bit.
### SEERS
During it's conception and development, we considered the societal implications of The WindUp:
#### Sustainability
For the housing, we used laser-cut acrylic which is recyclable and 3D printed PLA which is biodegradable. Our modular construction means disassembly is easy, so the housing can be recycled without the electronics. This aspect of the design also means replacing any broken parts of the housing is possible. We can also provide the 3D model files, which means replacement parts can be laser-cut or 3D-printed. This can extend the lifespan of our product and lessens the need to buy a full replacement.
#### Ethics
All of our code will be open-source, as well as any borrowed code being sufficiently referenced and credited. We will also make our parts list available, to ensure transparency on where we source our materials and components. We will also keep in mind the instruments cultural standing as the hurdy gurdy was historically a church instrument, so the product won't depict any religious or political imagery.
#### Equality and Inclusion
Both the handle and the body of our product are made ergonomic to ensure handling it is comfortable. However, with the inherent design of a hurdy gurdy, users with mobility issues may struggle with its usage. Depending on what level of the product is sold, we offer a range of price points to ensure accessibility in a financial stand point.
#### Risk
The pre-built kit will have any sharp corners sanded down, and the self-assembled kits will have instructions to do so in the assembly manual. The modular connections have been tested to ensure the structural integrity of our product, however this can be adjusted in the 3D model when manufacturing the housing. However, we are still looking into being able to suitably protect the electronics from environmental factors. 
#### Security
As stated before, our code will be open-source, so participants can identify any potential security vulnerabilities in the code. The WindUp will also not be connected to the internet as well as not having any digital inputs to prevent malicious software being installed. There aren't any digital outputs, so we won't be able to collect user data. The housing is also able to be secured to make malicious modifications more difficult, however the modular design of both the housing and circuitry means the product is still prone to tampering.
### Peer Review
#### Marcy (23 shares)
- Marcy was the Hardware Lead, and led the manufacturing portion of our product, including designing the circuitry hardware and modelling, the housing.
- She was also played a very instrumental role by being the Creative Lead in the ideation stage of the project, pitching multiple ideas for instruments and physical user interfaces.
- As she had the most technical knowledge and experience behind circuit design and manufacturing, so she led a lot of the hardware section by herself, however she could've delegated tasks to Alex or Felix.
#### Dylan (19 shares)
- I was the Programming Lead and managed the software aspects, including setting up GitHub repositories, coding the logic for the button matrix and menu system.
- I also collated everyone's code, and guided anyone who programmed to use consistent naming when using repository branching and pull requests. 
- I also worked heavily on the Tender Presentation Video, as well as the upcoming Demonstration Video, where I animated, sound designed, and video edited all of it. I also refined Marcy's original logo idea, as well as developing a company visual identity.
#### Korede (18 shares)
- Korede helped out on programming, and wrote code for calculating the crank's rotational speed and acceleration.
- He also wrote summaries on Dave's STM32 notes, which greatly benefitted all the programmers. 
- Although he completed all of his tasks, he sometimes struggled with communication on what's been completed.
#### Alice (17 shares)
- Alice was the Project Manager and Secretary, who set up meetings, tracked meeting minutes, and organised our group's Google Drive.
- She was able to keep a lot of the group accountable with assigning rough tasks and goals for everyone.
- She also helped writing scripts and directing the voiceovers for the Tender Presentation Video.
#### Alex (16 shares)
- Alex was assigned to work on hardware with Marcy. He was able to 3D model a casing for the D-pad in CAD. 
- He also gave some agency when writing scripts for the Tender Presentation Video.
- He was vocal about wanting more work, however Marcy handled a lot of the hardware work herself.
#### Felix (9 shares)
- Felix was assigned to be Hardware Lead, however relinquished the role to Marcy a few weeks, and instead chose to work on the audio synthesis aspect of the programming. 
- He helped contribute ideas in the ideation stage, as well as company names.
- However, he didn't show up to a few meetings without warning, and we had to ask our supervisor for a welfare check. We also haven't seen any evidence of the code yet.