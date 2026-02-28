---
dateCreated: 2025-12-21 20:03
---
[Module:: [[Communication Systems and Digital Communications]]]

Reliable [[communication]] is important for many applications, which means we need to reduce errors. Of course, it's impossible to avoid errors all together, as the probability error of error never reaches zero. Usually, we specify a tolerable [[bit error]] rate for each type of data. So, how do we minimise errors?
```table-of-contents
```
---
## Dealing with Errors 
If errors occur, there are several options:
- Do nothing, and tolerate their effects
- Detect and discard affected data
- Detect and correct 
- Detect and/or fail to correct, and request retransmission
The best approach depends on many factors, more notably the application requirements and channel characteristics. Which method meets the application's requirements? Which method might utilise fewer resources?
### Choosing an Approach
How do we choose between error detection, and error correction? 

If we have channels that are subject to highly variable (burst) error rates, or short range [[Wireless Links|wireless links]], it might make sense to just detect the errors and retransmit the [[signal]]. If we have the opposite, with less variable error rates and longer range [[wireless links]], then error correction might work better. 

Retransmission is pretty good, and we can approach nearly completely reliable [[transmission]]. However, it requires a return channel to signify when a retransmission is needed, and retransmission can add a theoretically unbounded delay, as we can't predict how many times the system has to retry the [[transmission]]. If it's time critical, then retransmission would introduce an excessive delay. 

Using both will often be sensible in practise, where error control coding may deal with typical operating conditions, and retransmission is used as a backup.
## Error Control Coding 
...is concerned with adding redundancy to the transmitted [[information]] for the purpose to detect and correct errors. The father of communications, Claude Shannon, stated that the capacity of a channel could be reached with an arbitrary low decoded error probability, with suitable forward error correction codes. 

In other words, every communication channel has a maximum "speed limit", called the **channel capacity**. If you send data *slower* than this limit, it's possible to achieve nearly error-free communication. 
### Detecting Errors 
There are a few methods to detect errors:
- Simple parity check
- Checksum 
- Cyclic Redundancy Check (CRC) 
These methods all act on groups of bits, implying the data stream is divided into packets. It's impossible to detect an error in a single isolated bit. All of them add more bits to the packet that enable them to check the rest of the packet for errors. 
### Correcting Errors 
Similarly, there are multiple ways to correct errors, with variations on each technique:
- Block codes, which operate on fixed block-by-block basis
	- Repetition codes
	- Multiple-parity check codes 
	- Hamming codes
	- Reed-Solomon
	- Bose-Chaudhuri-Hocquenghem (BCH)
	- Low density parity check (LDPC)
![[Error Control Coding.png]]

- Convolutional codes, which operate of arbitrary block lengths with a sliding window
	- Turbo codes
- Non-linear codes 
![[Error Control Coding-1.png]]
#### Complexity 
Encoding is simple. Decoding is complex! We may have to search through a very large set of codewords for the most probably codeword. There's always a trade-off between coding gain, and decoding complexity. A large part of coding research has been to find codes with a computationally feasible decoding algorithm. 
#### Latency 
Since a code operates on messages containing many bits, there is an inherent latency given by the number of bits being operated at any time. There may also be an additional processing delay due to limitations of decoder speed, and there's another trade-off between latency and coding gain.
## Burst Error Correction Capability 
Some channels change over time (like a phone signal dropping when you walk past a building), as the [[signal|signals]] can arrive at the receiver at different times due to reflections, called multipath fading. Most codes operate most effectively with random errors, and fail when faced with a "burst", like a whole page being missing from a book. 

To fix this, we can make a bursty channel *appear* random, using **interleaving**. The affected bits are spread out over time so a code can deal with it, then it's de-interleaved to bring it back to the original data.

![[Error Control Coding-2.png]]
## Block Codes
We can package raw data before [[transmission]] to protect it from errors. 

![[Error Control Coding-3.png]]

Here, we have a code with length $n$ codewords, including $k$ data bits (the original [[signal]]), and is referred to as an $(n,k)$ code.  
### Code Rates
The rate or efficiency of a code $R$ is the number of information bits $k$ divided by total number of code bits $n$. It basically tells us the ratio of actual data, and redundancy. It's simply:
$$R= \frac{k}{n}= \frac{\text{Information Bits}}{\text{Total Bits}}$$
- $R \rightarrow 1$ means mostly informational data is sent, with little protection. It's fast, but risky if the channel is noisy.
- $R \rightarrow 0$ means most informational data bits have a corresponding protection bit. Reliable, but consumes a lot of bandwidth. 

Having more bits means we need more bandwidth; we need more room on the channel to send the same amount of real data. The formula for **overall bandwidth efficiency** is:
$$\begin{align}
W &= \frac{r_{b}}{\eta_{\text{mod}}} \cdot \frac{n}{k} \\
\eta_\text{total} &= \frac{r_{b}}{W}= \frac{\eta_\text{mod} \cdot k}{n}
\end{align}$$
- $r_{b}$ is our desired data rate
- $\eta_\text{mod}$ is the efficiency of our modulation bandwidth (how dense the signal is)
- $\frac{n}{k}$ is the inverse of our code rate, which accounts for the lost efficiency from adding the error correction.
## Packet Length 
Each header in every packet have check bits. The probability of at least one error in a packet of length $N$ bits, if [[bit error]]s occur independently with probability $p$:
$$\begin{align}
P_\text{error} (\text{packet}) &= 1- P_\text{noError}(\text{packet})=1-(1-p)^{N} \\
p &= 1- \sqrt[N]{1-P_\text{error}(\text{packet})}
\end{align}$$
## Hamming Distance
Consider a 2-bit message, that has three check bits to each. For 2 information bits, there are 4 possible messages, to each of which we may add a combination of check bits, forming a set of 4 **codewords**.
![[Error Control Coding-4.png]]

Correction power is simply the number of errors (t) per codeword a code will correct. The Hamming distance measures the "closeness" of words, defined as the number of places in which two words differ.
![[Error Control Coding-5.png]]

The **minimum** Hamming distance $d_\text{min}$ of a code is the smallest Hamming distance between any pair of its codewords. A code will guarantee to:
$$\begin{align}
\text{Detect:} \quad &t<d_{\text{min}} \space \text{errors}\\
\text{Correct:} \quad &t<\frac{d_{\text{min}}}{2} \space \text{errors}
\end{align}$$
If our code has a $d_\text{min}$ of 3, you can detect up to 2 errors (as $2<3$) however can only correct 1 error ($1<\frac{3}{2}$)
### Singly Parity Check Codes
Let's add a single parity bit to the data, to make the total number of "1"s even, which is called even parity. Fore example, if we have $0 1 1 0 1 0 1 1$, we have an odd number of $1$'s. The parity bit will be $1$. to make it even, so the transmitted packet is $01101011|1$. If there's an error either in the parity bit of information bits, there will be an odd number of $1$'s and an error will be detected. 

Two codewords must differ in at least two places, as one bit difference would change the parity. The code is $(n,n-1)$.  
### Multiple Parity Check Codes
Single parity don't correct errors, but multiple parity can correct a limited number of errors in a packet.
![[Error Control Coding-6.png]]
## Hamming Codes 
Hamming codes are linear block codes that will correct any single errors and detect double errors. Add $n-k$ (total - data) parity check bits, so that each parity check covers a different combination of bits. Then single [[bit error]] results in a different combination of parity failures (called a syndrome), allowing errors to be located and corrected.
### Encoding 
Determines the combinations of data bits to be checked by each parity bit. Each data bit must be checked by a unique combination of at least two parity bits.

![[Error Control Coding-7.png]]
### Minimum distance 
Consider the effect on the corresponding codeword of changing bits.
- Changing 1 bit changes at least 2 parity bits, as each data bit is checked by at least 2 parity bits.
- Changing 2 bits changes at least 1 parity bit, no pair of bits are checked by the same combination of parity bits.
So, the minimum distance is 3, and the code can:
- detect one or two [[bit error]]s 
- correct single bit errors.