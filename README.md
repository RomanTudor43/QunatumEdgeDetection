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

# Quantum Hadamard Edge Detection (QHED)

The Hadamard gate $H$ has the following operation on the state of a qubit:

$$ |0\rangle \rightarrow \frac{|0\rangle + |1\rangle}{\sqrt{2}} $$
$$ |1\rangle \rightarrow \frac{|0\rangle - |1\rangle}{\sqrt{2}} $$
It creates an equal superposition of the basis states when applied to $|0\rangle$ or $|1\rangle$.


For two neighboring pixels, the bit-strings can be written as $|b_{n-1}b_{n-2}...b_10\rangle$ and $|b_{n-1}b_{n-2}...b_11\rangle$ 

To optain this we apply a H gate on the LSB.
The operation $I_{2^{n-1}} \otimes H_0$ can be represented by the matrix:

$$ I_{2^{n-1}} \otimes H_0 = \frac{1}{\sqrt{2}} \begin{pmatrix}
1 & 1 & 0 & 0 & \dots & 0 & 0 \\
1 & -1 & 0 & 0 & \dots & 0 & 0 \\
0 & 0 & 1 & 1 & \dots & 0 & 0 \\
0 & 0 & 1 & -1 & \dots & 0 & 0 \\
\vdots & \vdots & \vdots & \vdots & \ddots & \vdots & \vdots \\
0 & 0 & 0 & 0 & \dots & 1 & 1 \\
0 & 0 & 0 & 0 & \dots & 1 & -1
\end{pmatrix} $$

This matrix describes applying the Hadamard gate ($H_0$) to the last qubit (qubit 0) while leaving the other $n-1$ qubits unchanged (represented by the identity matrix $I_{2^{n-1}}$). The $\otimes$ symbol denotes the tensor product.

When this operation is applied to a state vector with amplitudes $c_0, c_1, c_2, \dots, c_{N-1}$ (where $N=2^n$), the transformation is as follows:

$$ (I_{2^{n-1}} \otimes H_0) \begin{pmatrix} c_0 \\ c_1 \\ c_2 \\ c_3 \\ \vdots \\ c_{N-2} \\ c_{N-1} \end{pmatrix} \rightarrow \frac{1}{\sqrt{2}} \begin{pmatrix} c_0 + c_1 \\ c_0 - c_1 \\ c_2 + c_3 \\ c_2 - c_3 \\ \vdots \\ c_{N-2} + c_{N-1} \\ c_{N-2} - c_{N-1} \end{pmatrix} $$


Following these stpes we have gradient between the pixel intensities of neighboring pixels in the form of 
where i is even ( 0 & 1 ,2  2 & 3 ).

For detecting horizontal boundaries between odd-pixel-pairs ( 1 & 2 ,3 & 4 ) apply same steps on $(c_1, c_2, c_3, \dots, c_{N-1}, c_0)^T$.


