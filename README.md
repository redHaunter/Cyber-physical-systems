# [Dimension Reduction](https://users.encs.concordia.ca/~wlucia/files/DimReduction_Mehran2023.pdf)
## Cyber-Attacks
Cyber-attack detection strategies generally can be defined into two groups:
- ### Passive
    - Can detect False Data Injections (FDI) but it is unable to detect more intelligent and dynamic ones
- ### Active
    - These strategies modify the system's I/O dynamically to detect attacks. Some strategies are:
        - Watermarking: By authenticating the I/O of the system can detect replay attacks
        - Moving target: Avoids systems identification and limits attacker's plant model knowledge
        - Sensor-coding: Prevents injection attacks related to unstable eigenvalues of a system by encoding the sensor measurements

## Novelty
Since the proposed strategies are lossless and follow specific mechanisms, the encoded data contains the same data as the raw format. By that, the attacker may find the encoding/decoding mechanism and, therefore attack the system. So, a time-varying encoding mechanism is proposed based on three concepts:
- principal components (PCs) analysis
- dimensionality reduction
- optimal reconstruction

#### Cyber-Attacks models:
1. False data over communication channels
2. Disturb the actuation channel by injecting false values, replaying previously recorded data over the sensor channel (stealthy replay)
3. Again disturbing the actuation channel by false value injection, only this time intelligently inject the sensor channel to remove the effect of disturbing (covert attacks)

#### Dimension Reduction
Sensor measurements get a dot product with an orthonormal matrix which tries to minimize the reconstruction error between the raw measurements and the transformed one. This optimized matrix is computed using the normalized consecutive number of samples over time from sensors (*Principle Components*).
> This encoding also reduces noise data measurements 

#### Unknow Input Observer (UIO)
Here, a dynamic model is represented to estimate the reconstruction error while it estimates the system's state simultaneously. This model (UIO) ensures the stability of the system by dynamically evaluating a bounded reconstruction error.

#### Anomaly Detection Design
Leveraging on decoded output signals, the upper and lower bounds of the UIO's variable can be evaluated by probability. This way a Gaussian model can be represented for detecting anomalies in signals.
> The proposed PDF gets compared to a threshold, in order to be detected as an anomaly

#### Encoding Schema for Stealthy Attacks

1. Encoding matrix chooses randomly (seed)
2. Augmented vectors of outputs are constructed
3. A permutation matrix is applied to the augmented vector to define which output is transmitted

**Note**: On the other hand, the decoder, performs the vice-versa to extract the output signal


# [Backward Reachable Sets (BRS) for Predictive Control](https://users.encs.concordia.ca/~wlucia/files/DataDrivenROSCMehran2023.pdf)

A data-driven approach is proposed to compute BRS for zonotopic representation
> Also a novel description for the computed BRS is proposed, in addition to the ST-MPC obtained from previous works

#### Problems that the proposed novelties have met:
1. Set intersection operation is required to calculate BRS because zonotopes are not closed under the Minkowski difference
2. Exponential number of constraints
> An additional advantage of the proposed ST-MPC is that it can be achieved from previously computed BRS (offline)

### ST-MPC	
Defining Robust Control Invariants (RCI) as a subset of states that satisfies a certain number of control variants for a discrete-time linear time-invariant system under any state and disturbance variants.
With this plant model, a ST-MPC can be designed in offline and online approaches. This way, the algorithm has two properties:
- It can be optimized recursively
- The desired subset is achievable in at most of few steps

### Algorithms
With the given system representation and noise consideration in section 3.A, the ROSC can be computed using Minkowski sum/difference. Then the desired subset of states in zonotopic representation can be computed.
> The above solution has a scale issue in the computation for deriving the ST-MPC algorithm, therefore an augmented zonotopic representation is proposed

The desired augmented space is computed with a projection operation over the states. Now with this augmented ROSC, the ST-MPC as a data-driven controller algorithm can be computed in both online and offline approaches, and also be proven to work. 
