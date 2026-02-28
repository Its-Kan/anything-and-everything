[[Year 1]]
[[Electrons in Solids I]]
## Electrons

First things first, electrons in solids behave differently from electrons in free space. Crazy. For now, let's define electrons as small negative charges orbiting around the positively charged nuclei.

You know about the Classical Model of an atom (electrons orbit due to the electric force which have less potential energy nearer the nucleus), but that kinda breaks down with quantum mechanics (yay, your favourite). Not predicted by the classical model:

- Electrons can only be in certain "orbits" with certain energy levels. These orbits are grouped into shells, where the first shell has 1 possible orbit, second shell has 4, and third has 9.
- No more than two electrons can be in the same "orbit" at the same time.

**Valence electrons** are those in the highest energy occupied states, so are weakly attracted to the nucleus and are easily effected by other atoms nearby. Ok cool, let's put two atoms together. 

But only two electrons can be in the same orbit, *I literally just said that*, so what happens? The energy levels slightly split, so they're very slightly split. However, it's very likely some might move up to the next energy band *when it's not absolute zero*. This means electrons can easily move between different states, and hence move through the solids. More atoms, more states. When we get a lot more atoms, we then get a lot more states. At some point, it just looks like a band of energy levels.
## Fermi-Dirac Distribution

Let's look at a single electron. Because of quantum mechanics, we can't exactly say where it is, but we can calculate the probability of what band it's in. This is where the Fermi-Dirac Distribution comes in!

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240515010622.png]]
### $p(E) = \frac{1}{e^{({E-\eta}/{kT})}+1}$ 
- $p(E)$ is the probability of an electron at a specific energy state
- $e$ is the charge of an electron
- $E$ is the energy of the level the electron *could* be in
- $\eta$ is the Fermi level
- $k$ is the Boltzmann constant
- $T$ is the temperature

At any temperature greater than absolute zero, electrons may be in any state (cause like, quantum). If E = $\eta$, then E = 0.5, which  is the Fermi level. This is the state where the probability of occupation WOULD BE a half. However, there doesn't necessarily need to be a state at the level. This is why the _would be_ in the previous bullet point. 

Being above the Fermi level means it's less likely there's an electron in that point, and being below means the opposite. Anything in the range in-between 1 and 0 means there are more possibilities of electrons moving. If the range is in an empty space in the bands, then its impossible for the electrons to move. If the range crosses a band, then this range has a high likelihood for electrons to move into these levels, and are therefore more conductive. Think of this range as the range where electrons can jump. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240515012711.png]]

## Valence and Conductive Bands

Let's talk about bands. The valence band is the outermost electron shell, and is the highest range of electron energies where electrons can be present at absolute zero. This means it's below the Fermi level. Think of it as the most filled seats. The conduction band is right above the valence band, and is the lowest range of electrons; they are less likely for an electron to occupy it. 

C is a conductor. The valence band is partially filled, so with some thermal energy, electrons can move and the energy can be conducted purely in the valence band. 

B is an insulator. As the range doesn't coincide with any of the bands, no electrons can move.

A is a semiconductor. It has a small band gap, and some electrons are able to jump into the conductive band. Some electrons can move, by electrons jumping levels, which means energy can be conducted.

## Semiconductors

To make a semiconductor more conductive, we can dope it, by adding different elements to the lattice with more or less electrons. 

**N-type semiconductors** adds electrons to the bottom of the conduction band. These electrons can move, and conduct electricity

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240515014154.png]]

**P-type semiconductors** removes electrons from the top of the valence band, so electrons can move into that level.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240515014330.png]]

In both cases, we're pushing a little closer to the Fermi level, just so electrons are more likely to move. 
## Ohm's Law

Ok, change of pace, and let's zoom out. In terms of electrons, why does Ohm's law work? We will need to have a model for electrons in a metallic conductor: The Drude Model.
- Electrons do not interact with each other
- Electrons "bounce" off nuclei, and are equally likely to bounce in any direction
- New definitions:
	- $\tau$, average time between collisions
	- $n$, density of electrons (electrons/$m^{3}$)

LETS DO SOME MATHS SHIT.

$Force = Eq = m_{e}a$, so $a = \frac{Eq}{m_{e}}$.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516211011.png]]
