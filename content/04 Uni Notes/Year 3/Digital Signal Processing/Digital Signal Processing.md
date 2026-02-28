---
tags:
  - uni/year3
---
> [!uninotes] Digital Signal Processing
> ```dataview
list
from "04 Uni Notes/Year 3/Digital Signal Processing"
where file.name != regexreplace(file.folder, ".*/", "") 
sort regexreplace(file.folder, ".*/", "") asc
> ```

```meta-bind-button
label: Create New Note
icon: plus
style: primary
class: ""
cssStyle: ""
backgroundImage: ""
tooltip: ""
id: ""
hidden: false
actions:
  - type: templaterCreateNote
    templateFile: 02 Templates/Uni Notes Template.md
    folderPath: 04 Uni Notes/Year 3/Digital Signal Processing
    fileName: Untitled Uni Note
    openNote: true
    openIfAlreadyExists: true

```

## Introduction 
DSP is concerned with the representation of signals by sequences of numbers or symbols, and the processing of these sequences. 

Analogue signals are continuous, and aren't sampled. Digital signals are discrete, with specific measurements at certain intervals. 
- Continuous will be represented as $x(t)$ in the [[time domain]] and $X(f), X(\omega)$ in the [[frequency domain]] .
- Discrete is $x[n]$, and $X[k]$ where $n, k$ are integers. Time is discrete, where $t_n = n \Delta t$, where $\Delta t$ is the sampling interval. As well as discrete frequencies. 
## [[Fourier Transforms]] 
Takes a [[signal]] $x(t)$ and outputs the frequency content of said signal, $X(\omega)$

We have multiple types in this course: 
- [[Fourier transform]] (FT), which has continuous time and frequency
- [[Discrete time Fourier transform]] (DTFT), which has discrete time, but continuous frequency
- [[Discrete Fourier transform]] (DFT), which has discrete time and frequency 

