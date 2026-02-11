# Quantum Repetition Code

Given that we have already seen the [Classical Repetition Code](./01-repetition-code.md) we can now take the first leap into a quantum code. This code is represented by basically the same theoreticall principel. However, the way the decoding process works is interpreted with a diferent lens because we do not have the same information duplicated in every qubit. Rather we have the information distributed in all three qubits.

The first thing that defines this code is the way the encoding works. In the classical code the bit could be simply duplicated, something that is imposible in quantum computing. Nonetheless we do have a linear operator that encodes a qubit into three others. It is represented by the circuit represented by [](#quantum_repetition_code_encode_circuit)

```{figure} ../images/quantum_repetition_code/01_encode_circuit.png
:label: quantum_repetition_code_encode_circuit
:alt: Circuit that encodes the quantum repetition code, It's basically a 3 qubit circuit where the first entry is a state $\ket{\psi}$ and the other two are $\ket{0}$ and two CNOT gates both with the control in the first input but with the not on other side
:align: center

Circuit that encodes a Qubit in an equivalent way it would in the classical repetition code. This shows that this code is possible for the existence of a linear hermitian process that encodes the information.
```

The decoding process for this code is equivalent to the classical. Meaning that it is projecting into

* $P_0 = \ket{000}\bra{000} + \ket{111}\bra{111}$ No error happenend
* $P_1 = \ket{100}\bra{100} + \ket{011}\bra{011}$ There was an error in the first qubit
* $P_2 = \ket{010}\bra{010} + \ket{101}\bra{101}$ There was an error in the second qubit
* $P_3 = \ket{001}\bra{001} + \ket{110}\bra{110}$ There was an error in the third qubit

This way we can recreate the original qubit by apliying the contrary operation of the error. The 
