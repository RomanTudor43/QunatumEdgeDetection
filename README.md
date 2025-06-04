# QunatumEdgeDetection
## Quantum Probability Image Encoding (QPIE)
	
The QPIE representation uses the probability amplitudes of a quantum state to store pixel values of a classical image. Quantum amplitude encoding loads classical data into a quantum state by using the data values as amplitudes of a superposition state.

For example, with a 2×2 matrix the quantum state is:

$$ |\psi\rangle = c_0|00\rangle + c_1|01\rangle + c_2|10\rangle + c_3|11\rangle $$

Each coefficient $c_i$ corresponds to a pixel intensity after normalization, calculated as:

$$ c_i = \frac{I_{yx}}{\sqrt{\sum I_{yx}^2}} $$

Here, $I_{yx}$ is the pixel intensity at position $(y, x)$, and the denominator normalizes the quantum state.

OR generalizing for $n$-qubits, we have,


$$ |Img\rangle = \sum_{i=0}^{2^n-1} c_i |i\rangle $$

This formula represents a quantum state, often used in the context of encoding an image, where:
-   $|Img\rangle$ is the quantum state representing the image.
-   $n$ is the number of qubits used.
-   The sum $\sum$ goes from $i=0$ to $2^n-1$, covering all possible computational basis states for $n$ qubits.
-   $c_i$ are the complex amplitudes associated with each basis state $|i\rangle$. The square of the magnitude of $c_i$ (i.e., $|c_i|^2$) gives the probability of measuring the state $|i\rangle$.
-   $|i\rangle$ represents the $i$-th computational basis state (e.g., for $n=2$, these would be $|00\rangle, |01\rangle, |10\rangle, |11\rangle$).

