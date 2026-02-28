---
dateCreated: 2025-10-07 20:23
---
[Module:: [[Communication Systems and Digital Communications]]] 

Why should we study this? It provides answers to fundamental questions, such as what information is, how we can represent data source efficiently, etc. It also paves the way to some very practical techniques, like source coding and error control coding.
```table-of-contents
```
---
## Intro 
Information theory comes from probability theory, as both are based on the concept of uncertainty. We use probability theory to deal with randomness. Probability is a measure of the likelihood of events, used to determine the information content of messages. 

Some useful terms...
![[experiment]]

![[event]]

![[mutually exclusive events]]

![[independent events]]


| Term                          | Definition/Description                                                                                                                                              |
| :---------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Information Theory**        | Derived from **probability theory** and based on the concept of **uncertainty**.                                                                                    |
| **Probability Theory**        | Required to deal with **randomness** in communication systems. It is a measure of the **likelihood of events** and is used to determine information content.        |
| **Experiment**                | An activity that is measured or observed, comprising a series of experimental trials.                                                                               |
| **Event (Outcome)**           | A possible outcome from an experiment.                                                                                                                              |
| **Mutually Exclusive Events** | Events that cannot happen together (e.g., rolling a die and getting a four or a six).                                                                               |
| **Independent Events**        | Events where the occurrence or non-occurrence of one event does not affect the probability of the others.                                                           |
| **Information Source**        | Must be **random (to some extent)** to convey information. Successive symbols are often independent.                                                                |
| **Radix**                     | The size of the alphabet of the information source.                                                                                                                 |
| **Permutation**               | An **ordered selection** from a group of objects; position is important.                                                                                            |
| **Combination**               | An **un-ordered selection** from a group of objects; position is not important. Useful for calculating probabilistic problems in communications (e.g., bit errors). |

| Concept                                 | Formula                                                                                     | Notes                                                                   |
| :-------------------------------------- | :------------------------------------------------------------------------------------------ | :---------------------------------------------------------------------- |
| **Basic Probability**                   | $$P(X) = \lim_{N\rightarrow\infty} \frac{N(X)}{N}$$                                         | $N(X)$ is the number of occurrences of $X$ in $N$ trials.               |
| **Sum of Probabilities**                | $$\sum_{i=1}^{M} P(E_i) = 1$$                                                               | The probabilities of all $M$ possible events ($E_i$) must sum to unity. |
| **Composite (Mutually Exclusive)**      | $$P(X \text{ or } Y) = P(X) + P(Y)$$                                                        | Used when $X$ and $Y$ cannot occur together.                            |
| **Composite (Not Mutually Exclusive)**  | $$P(X \text{ or } Y) = P(X) + P(Y) - P(X \text{ and } Y)$$                                  | $P(X \text{ and } Y)$ is the joint probability.                         |
| **Joint (Independent Events)**          | $$P(X \text{ and } Y) = P(X, Y) = P(X) \cdot P(Y)$$                                         | Used when $X$ and $Y$ do not influence each other.                      |
| **Joint (Non-Independent Events)**      | $$P(X \text{ and } Y) = P(X) \cdot P(Y, X) = P(Y) \cdot P(X)$$                              | Used when the outcome of $X$ affects the outcome of $Y$                 |
| **Conditional Probability/Bayes' Rule** | $$P(Y \vert X) = \frac{P(X \text{ and } Y)}{P(X)}  = \frac{P(Y) \cdot P(X \vert Y)}{P(X)}$$ | Used when two events are dependent                                      |


| Concept         | Formula                          |
| :-------------- | :------------------------------- |
| **Permutation** | $$_n P_r = \frac{n!}{(n-r)!}$$   |
| **Combination** | $$_n C_r = \frac{n!}{(n-r)!r!}$$ |
