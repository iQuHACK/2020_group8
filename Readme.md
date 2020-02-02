# Quantum simultion and entanglement entropy measurement of 2D transverse field Ising model


## Author: Group 8 (Otto)  $~~~~$   Date: 20200202
## Changhao Li, Mo Chen, Yi-Xiang Liu, Wenchao Xu, Calvin Sun (all equal contribution)

Quantum simulation is promising technique to tackle the problems that are unreachable for classical simulation in the field of quantum chemistry, condesed matter physics, material science and high energy physics. The most flexible strategy to achieve quantum simulation is via digital quantum simulation, where a target time-evolution operator is represented by a sequence of elementary quantum gates, which are usually one-qubit or two-qubit gates. The strategy of approximating the continuous evolution with discrete gates is also known as Trotter expansion. With realiable quantum processors and Trotter expansion techniques, one can simulate specific Hamiltonians, which might be unaccessible for analoge quantum simulations.

In the engineered quantum systems, entanglement is significant and provides signatures of a wide range of phenomena, including quantum criticality and topological phases, as well as thermalization
dynamics and many-body localization. Entanglement entropy can characterize the ammount of entanglement and usually require measurement of the full density matrix, which can take exponential long time for large systems. Recent experiments probed the Renyi entropy based on statistical correlations between randomized measurements, which can be more efficient than the quantum tomography techniques. 

In this work, we combine the digital quantum simlation with randomized measurement techinique to simuate two-dimensional transverse field Ising model (2D TFIM) with nearest neighbor coupling in IBM quantum processors. We first introduce an efficient method than can implement the 2D TFIM in the online IBM quantum computers based on Trotter expansion, and then work on probing the time growth of second-order Renyi entropy in different parameter regimes. Our protocol, if successfully implemented in the IBM 16-qubit processor, will provide an efficient method in studying the topological phases and thermalization of 2D TFIM model.

We begin with present the simulation circuits. We first consider an 2*2 qubit lattice for simplicity.  Note that the 2D TFIM reads:

$H_{TFIM} = \sum_{i,j}\sigma^{x}_{i,j}(J_{1}\sigma^{x}_{i+1,j}+J_{2}\sigma^{x}_{i,j+1}) + \sum_{i,j}h\sigma^{z}_{i,j}$

To implement the Hamitonian in the quantum circuits, we choose the basic Trotter elements as $\sigma^{x}\sigma^{x}$ and $\sigma^{z}$. In IBM 16 qubit register where two qubit gate can be only implemented via CNOT, we first decompose the $\sigma^{x}\sigma^{x}$ interaction between two qubits in the following circuits (which represents a $\pi/4$ rotation  $e^{-i \sigma^{x}\sigma^{x} \pi/4 }$):

![XX_circ.png](attachment:XX_circ.png)

The onsite operator $\sigma^{z}$ can be easily implemented with a rotaion along z direction. For example, when $J_{1}=J_{2}=h$, the  $\sigma^{z}$ term can be implemented with a $\pi/4$ rotation along z direction. The relative ratio between $J_{1(2)}$ and $h$ can be well tuned by adjusting the single qubit rotation angle along z direction. We consider The building block for a single Trotter step would thus be (the XX block represents the $\sigma^{x}\sigma^{x}$ interaction circuits shown above ):

![image.png](attachment:image.png)

We now proceed to the measurement of second-order Renyi entropy via randomized measurements. As in the protocol in $\href{https://science.sciencemag.org/content/sci/364/6437/260.full.pdf}{T. Brydgtes, Science 2019}$, we implement random unitary operations $U_{A}$ on qubits in the subsystem ($A$) that we are interested in, followed by measurements on the z-basis. The entropy can then be extracted via:

$S^{2}(\rho(A)) = -log_{2}\bar{X}$,   $X = 2^{N_{A}}\sum_{s_{A},s_{A}^{\prime}}(-2)^{-D(s_{A},s_{A}^{\prime})}P(s_{A})P(s_{A}^{\prime})$,

where $s_{A} (s_{A}^{\prime})$ is the basis states of partition A (for example, $s_{A} = 1001$ in a four-qubit subsystem), $D(s_{A},s_{A}^{\prime})$ is the Hamming distance between $s_{A}$ and $s_{A}^{\prime}$, $N_{A}$ is the number of qubits in the subsystem and the bar denotes the ensemble average of correlations of excitation probabilities $P(s_{A})=\langle s_{A}| U_{A}\rho_{A}U_{A}^{\dagger}|s_{A} \rangle $.

An example of the circuit in simulating the 2D TFIM and measuring the entanglement entropy would thus be (XXZ block represents one Trotter step):

![image.png](attachment:image.png)

We next present our simulation results. In the following we take at least two random unitary sets each time and repeat it for at least 100 times. We first characterize the time evolution of Renyi entropy, i.e., for different Trotter steps, as shown in the following plot. Here we simulate a 2*3 qubit lattice and take half the lattice as our subsystem.

![image.png](attachment:image.png)

We can then change the system system and find the final entropy as a function of subsystem size. After finishing the simulation and compare it with they numerical calculation, we can then upload the circuits above to the IBM online quantum computer and run experiments.


```python

```
