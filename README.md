# Quantum Compilation of a Multi-Input Toffoli Gate Using Variational Quantum Algorithms

This repository implements two variational quantum algorithms for learning a multi-input Toffoli gate (multi-controlled X) using PennyLane. The project follows the methodology described in the attached PDF report and reproduces both cost functions discussed in the paper.

# 📌 Project Overview

The goal of this project is to approximate a target multi-input Toffoli (multi-controlled X, MCX) gate using a parametrized quantum circuit (ansatz) trained via gradient-based optimization.

Two independent cost-function approaches are implemented.

---

## 1️⃣ Hilbert–Schmidt Test (HST) Method

This method minimizes the cost function

$$
C_{\mathrm{HST}} = 1 - \frac{1}{d^2} \left| \mathrm{Tr} \left( V^\dagger U \right) \right|^2
$$

where:

- $U$ is the target Toffoli unitary,
- $V(\theta)$ is the parametrized variational ansatz,
- $d = 2^n$ is the Hilbert space dimension for an $n$-qubit system.

This cost directly measures the overlap between the learned unitary $V(\theta)$ and the target unitary $U$.  
The minimum value $C_{\mathrm{HST}} = 0$ is achieved when the two unitaries are identical up to a global phase.

---

## 2️⃣ Observable Expected-Value Method

This method constructs the observable

$$
A_n = I - 2 \sum_k 
\left(
|\chi^{(k)}_{\mathrm{in}}\rangle
\langle \chi^{(k)}_{\mathrm{in}}| \otimes 
|\chi^{(k)}_{\mathrm{out}}\rangle
\langle \chi^{(k)}_{\mathrm{out}}|
\right)
$$

where:

- $|\chi^{(k)}_{\mathrm{in}}\rangle$ are computational basis input states,
- $|\chi^{(k)}_{\mathrm{out}}\rangle$ are the corresponding correct output states defined by the Toffoli mapping.

The cost function is defined as

$$
C(\theta) = \frac{\langle A_n \rangle + 1}{2}.
$$

The minimum value $C(\theta) = 0$ is achieved when the variational circuit $U(\theta)$ perfectly reproduces the correct input–output mapping of the target Toffoli gate.
