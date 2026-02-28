[Year:: [[Year 2]] #uni/year2]

---

```cardlink
url: https://notebooklm.google.com/notebook/8660685c-958b-4ec7-b37a-d45ec5ef1270
title: "Sign in - Google Accounts"
host: notebooklm.google.com
```

> [!uninotes] Control, Sensors and Instrumentation
> ```dataview
list
from "04 Uni Notes/Year 2/Control, Sensors and Instrumentation"
where file.name != regexreplace(file.folder, ".*/", "") 
sort regexreplace(file.folder, ".*/", "") asc

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
    folderPath: 04 Uni Notes/Year 2/Control, Sensors and Instrumentation
    fileName: Untitled Uni Note
    openNote: true
    openIfAlreadyExists: true

```
## Control System Design
This requires:
1. A set of design objectives, e.g.
	- Transient response
		- How quickly should I change state when asked?
		- Can it overshoot its target?
	- Steady state error
		- How accurately does it need to settle?
	- Stability
	- Other factors
		- Financial constraints
		- Certification requirements
		- Robustness
		- etc.

2.  A mathematical system model. 
	- Simultaneous [[Differential Equations]] 
	- We'll be looking at [[LTI systems]] (linear time invariant systems)
		- [[superposition|Superposition]]
		- [[homogeneity]] 
	- The system model will be a set of linear simultaneous [[Differential Equations]] 
		- Which means... we can use [[Laplace Transforms]]!

## [[Laplace Transforms]] 
As we know, it can:
- Convert linear [[Differential Equations]] into polynomials
- Replace the convolution integral with multiplication
Most of the control engineering will take place in the [[s-plane]]. 

Control engineering is about changing the behaviour of systems. This is specified in terms of the [[time domain]] response of a system to an input, most often a [[Step Response|step response]], $\frac{1}{s}$.
## Transfer functions
![[transfer function]]
## Unity negative feedback 
![[unity negative feedback|Unity negative feedback]]

