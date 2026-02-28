---
dateCreated: 2025-10-12 18:18
---
[Module:: [[Communication Systems and Digital Communications]]]

- [[Information]] concerns change. 
- Information theory allows us to quantifiably measure information content.
- And information content, is related to **SURPRISE**!
```table-of-contents
```
---
## Information
[[Information]] is the resolution of uncertainty. If we get a message that has something we already know, then we haven't gained any new information. Simply, [[information]] is a measure of what you learn that couldn't have been predicted. If the contents surprise us (meaning we've learnt something new), then information has been transferred. 

Surprise also involves uncertainty (it's not one if we're certain what's inside!), and since uncertainty is measured with probability, we can use [[Probability Theory]] here! Denoting information as $A$ gets us:
$$I(A) = f(P(A))$$
Where:
- $I(A)$ is the information content itself, for information $A$
- $P(A)$ is the probability of $A$ occurring, *before* you know the outcome. Before noise messes things up.
- $f(P(A))$ is a function that links the probability to the information. 

Let's imagine we had a message with two independent symbols, $A$ and $B$. As they're probabilities, we can infer:
$$
I(AB) = f(P(A,B)) = f(P(A) \cdot P(B))
$$
The information conveyed by two symbols should be the same as the sum of the information of each separately: 
$$
\begin{align}
I(AB) &= I(A) + I(B) \\
\therefore f(P(A) \cdot P(B)) &= f(P(A)) + f(P(B))
\end{align}
$$
To satisfy this last equation, let's let the equation be:
$$I(A) = \log(\frac{1}{P(A)})$$
So for any message containing length *n* bits:
- The number of possible messages is $2^{n}$
- The probability of each message is $\frac{1}{2^{n}}$
- The information content of each message is $I=\log(2^{n})$
## Entropy 
Consider a binary source (is either on or off), with probabilities $P(1) = p$, and $P(0) = 1-p$. 

[[Entropy]] (H) is defined as the average information rate of a source. For a binary source:
$$
\begin{align}
H&=P(1) \cdot I(1) + P(0)\cdot(0) \\
&=p \cdot \log_{2}\left(\frac{1}{p}\right)+ (1-p)\cdot \log_{2}(\frac{1}{1-p})
\end{align}
$$
But for a more general definition, for a m-ary source:
$$\begin{align}
H &= \sum^{m-1}_{i=0} P(A_{i})\cdot I(A_{i}) \\
&= \sum^{m-1}_{i=0} P(A_{i})\cdot \log_{2}(\frac{1}{P(A_{i})})
\end{align}$$
Entropy is at a maximum when all symbols are equiprobable, sp
$$H_\text{max}= \log_{2}(m)$$
## Redundancy 
The maximum information rate of a source is also the "apparent" rate. The difference between $H_{max}$ and the actual information rate is called [[redundancy]], $R$.
$$R=H_{max}-H$$