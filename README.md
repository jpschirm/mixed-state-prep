# Mixed Quantum State Preparation

Given a $2^n \times 2^n$ density matrix $\rho$ construct a Qiskit circuit with measurements that prepares $\rho$.
The main implementation is in `mixed-state-prep.ipynb`.

## Idea
  
The construction uses purification. First, diagonalize $\rho = \sum_i \lambda_i |e_i\rangle\langle e_i|.$
Then prepare the pure state
$|\Psi\rangle = \sum_i \sqrt{\lambda_i}\, |e_i\rangle |i\rangle.$
If the second register is measured and the outcome is ignored, the first register has density matrix $\rho$. Equivalently, measurements of an observable $\mathcal{O}$ on the first register have expectation
$\sum_i \lambda_i \langle e_i|\mathcal O|e_i\rangle=\text{Tr}(\mathcal O\rho)$.

## Implementation

The notebook contains:
- a QROM-based diagonal unitary construction;
- a recursive pure-state preparation routine;
- a mixed-state preparation function `mixed_state_prep(rho, d=10)`;
- verification code for pure-state and mixed-state preparation;
- a demo for $n=2$.

The pure-state routine first prepares the non-negative amplitudes using multiplexed $R_y$ rotations, then adds phases using a diagonal unitary. The code uses Qiskit convenience gates such as `mcry` and `mcx`; these represent multiplexed rotations and bit-string selection operations discussed in lecture and can be decomposed into one-qubit gates and multiplexed $Z$-type operations.

## How to Run

Open `mixed-state-prep.ipynb`and run the cells in order.
The main demo constructs a random two-qubit density matrix, prepares its purification, and verifies that tracing out the index register recovers the original $\rho$.

## Main Function

```python
mixed_state_prep(rho, d=10)
```
