## App Features
OddTime is an audio-based iOS app, designed to be a visualiser for rhythmic complexity, aimed at ambitious musicians and producers who want to broaden their rhythmic horizons without requiring knowledge of sheet music. The app translates concepts such as polyrhythms, irregular time signatures and tuplet swing into intuitive, grid-based visualisations. The app is designed with UI and UX as a priority. The following are the app's key features:
- **Onboarding**: When the user opens the app, an onboarding tutorial should appear welcoming the user to the app, and guiding them on how to use it. This can be skipped if desired. 
- The app is organised into tabs, one for the visualiser, which is the default selection, and the other for settings. 
	- **Visualiser** the main visualiser view is split into two sections: the polyrhythm grid and the controls. The grid is a useful way to visualise polyrhythms, where the pink cells represents pulse one, and the purple cells represents pulse two. The values for each pulse can be adjusted with the two drop-down menus, and can be switched around using the button in-between them. The tempo can also be varied using the slider, and the sequence can be played using the play button. 
	- **Settings**: The settings tab has multiple options that can be changed such as light/dark mode, metronome sound (cowbell, wood click, hi-hat and kick & snare), master volume, and the ability to redo the tutorial if needed.
## Design
The app is coded in Swift using *SwiftUI* and *AudioKit*, and structured using the Model-View-ViewModel (MVVM) architecture. This isolates the raw data, application logic and user interface into separate components, allowing easier testing and readability. All UI and UX was planned out and designed in Figma to have a concrete idea of the visual identity of the app, which was then recreated in *Swift* using *SwiftUI*. 
### Assets
The Assets folder holds all the audio samples used in the app, including a text file with credits. All sound files are sourced from Pixabay. 
### App
The App folder holds the top-level *ContentView*, which collates all the child views into a *TabView*, as well as initialising and passing on managers to those views. 
### Managers
The Managers folder holds all the ViewModels for the app. These files handle the internal logic of the application, both observing the Views for changes in UI to update Model data, and handles logic of any data. They also declare *@Published* variables to broadcast and store app states.
- **AudioManager** manages and controls all aspects of audio, including setting up an *AudioEngine*, and MIDI callbacks, loading samples, creating samplers and sequencers, and plays samples back.
- **OnboardingManager** handles the logic for the onboarding tutorial for the app, including defining onboarding steps, and the progression through said steps.
- **PolyrhythmManager** handles the logic for the polyrhythm grid, including implementing the polyrhythm model data, generating a grid, and implements/adjusts the sequencer in *AudioManager*.
### Model
The Models folder holds all the Models for the app. These files store and define the raw data for the app.
- **Appearance** holds the data for the app's appearance, including light/dark mode and extensions to *View*, to add custom, pre-set styles and appearances.
- **Cell** holds the data for a single cell in the polyrhythm grid, holding its style, a unique ID and if the cell is active or not.
- **Onboarding** holds the data for an onboarding step, including a unique ID, a title, description and icon.
- **PlaylistCategory** is unused in v1.4.0, but would hold the data for different playlists in the upcoming Library feature.
- **RhythmPattern** holds the data for different patterns for the various rhythmic ideas, including metadata for polyrhythms (implemented already), and irregular time signature and tuplet swing (yet to be implemented). 
- **Song** is also unused in v1.4.0, but would hold the data for a song which holds a pattern, and relevant metadata to be showcased in the Library feature. 
### Preview Content
The Preview Content holds the colour palette for the app.
### View
The Views folder holds all the Views for the app. These files renders the Model data into an interactive UI, as well as holding controls to manipulate the data.
- **LibraryView** is unused in v1.4.0, but would display songs collated in playlists, that can be opened into the visualiser tab.
- **OnboardingView** displays the onboarding tutorial layered on top of the **ContentView**, in multiple steps.
- **SettingsView** displays a *ScrollView* of various settings that can be changed, including light/dark mode, metronome sounds and re-doing the tutorial.
- **VisualiserView** displays the polyrhythm grid, and controls to adjust it.
## Market Testing
From your market analysis, list the critical assumptions/hypotheses you chose to test in  
SimVenture validate. What made you choose these tests? Discuss and reflect on the  
findings from your market testing. What does that tell you about the commercial prospects of  
your app?  

Two surveys were conducted, to ascertain the market viability of the app, as well as visual design/app preferences.
### Market Research
This survey was sent to a Discord community of music producers and performers with varying expertise and specialisations, as the app's demographic is solely focused on musicians. It aimed to test the assumption that musicians want a tool to aid in visualising, performing and/or understanding complex rhythmic ideas. The following BMC Blocks were tested:
- **Customer Segment**: to ascertain the type of musician willing to use the app
- **Channels**: to find how best to reach users. 
- **Value Proposition**: to confirm whether the app will fill the user's needs
- **Get Keep Grow**: to explore what user onboarding will be most effective  
- **Revenue**: to discover how users are willing to pay for the app.

From the 23 responses received, 65.2% of respondents rated interest in the app based of its description a 4 or 5 out of 5, so the app is likely viable. Most respondents were aware/versed in complex rhythmic ideas (average of Very Comfortable), so the app should focus on honing these skills, rather than solely introducing beginners. However, they use these concepts much less frequently in their actual work (average of Neutral), so the app could also pivot to being a tool to generate and apply musical ideas using these rhythmic techniques. 

Majority of respondents (73.9%), use Android as their primary OS for their mobile device, so a port for the platform may be considered in the future. In terms of UI/UX, an overwhelming majority (87.0%) preferred a familiar grid-based sequencer, so the app will be designed similarly to a DAW's piano roll. Respondents also rated their most valuable features they want in the app, the top three being creating/saving custom patterns, the visualiser itself, and automation, so these were prioritised for the prototype.
### UI/UX Design Feedback
This survey was created after the initial market research form and the first prototype, sent to individuals who have shown interest in the app, and consented into being contacted again to give feedback. It aimed to test the assumption that musicians prefer easy-to-use, intuitive tools with a minimalist interface to better focus on usability. The one BMC Block was tested:
- **Value Proposition**: to explore what design choices will be the most desirable for the user.

From the 4 responses received, there was one performer, two producers, and one who did both, so the app will. When asked about frustrating parts of programming complex rhythms in their current software, two responders said tuplets/polyrhythms needed to be "drawn manually with big workarounds," which is a problem the app aims to solve. In terms of basic visual defaults:
- Respondents preferred a minimalist, modern and purely digital interface in dark and portrait mode. Designs that are too distracting or mimicked physical hardware (skeuomorphism) will be avoided.
- Performers placed their device at eye/waist level, so the UI should be easily seen and interacted with at a distance. Producers had a split in their preferences in app usage and input
- A split-screen layout was also preferred, so all controls are visible on one screen. There was a split in how respondents preferred the two pulses in a polyrhythm to be distinguished, either between separate colours or separate shapes. An option to toggle between both will be added to provide maximum clarity.
- Respondents preferred a wood click as the default sound, as well as preferring to type specific values for the tempo. This will be added along with the common slider input.
- For the song library, respondents were comfortable loading their own local audio files to sync with the visualiser, to avoid licensing issues. 
## Future Development
Following your market analysis and concept testing in SimVenture Validate, explain how your  
App could be developed in the future. Using evidence from your research, describe new  
features, and improvements you might consider to the existing operation to further improve  
the commercial potential of your app and attract bigger market segments.

The app has been coded with future development in mind, including using the MVVM architecture, and object-oriented programming techniques to ensure easy modification or alteration in the code for future updates/patches.

Following the results of the UI/UX Design Feedback survey, the most highly valued potential feature respondents wanted to see in the app was the ability to create and save patterns. 
- The next main release for the app will focus on implementing the Library feature of the app. This would add another tab to the interface, which would be organised in horizontal carousels, stacked vertically. The user can access their saved patterns, as well as browse playlists of songs that utilise complex rhythmic ideas. The infrastructure for the feature already exists, with the *VisualiserView* and *Song* model, however the views for the carousel and song card need to be developed.
- The song presets will require the automation feature to be added, which allows the visualiser to be changed over time, which is important if a song has rhythmic changes throughout. A rework in how the data for individual patterns might have to be introduced, likely using JSON files to track what changes are in a song. 
- To tie-in with the social media aspect of the app's marketing plan, a simple export to video option will allow users to advertise the app themselves by sharing their patterns to social media. 

In order to reach a larger market segment, the app will be advertised via short form video content showcasing the app, synced to popular . Videos showcasing visualisations of complex rhythmic ideas, have a niche but popular following on video-sharing platforms, with a dedicated userbase already interested in this aspect of rhythmic visualisation.
- 17a's visualisation of Toby Fox's "The Third Sanctuary" that use changing irregular time signatures has 737k views on YouTube.
- project.jdm's creative polyrhythm visualisations on Instagram accrue thousands of likes per post.
- IJ & phonon have a substantial following on multiple platforms including TikTok, Instagram and YouTube, where they showcase creative uses of both polyrhythm and tuplet swing in their own music alongside visualisations.