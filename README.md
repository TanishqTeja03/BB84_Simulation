# BB84 Quantum Key Distribution Simulator

This project provides a Python-based simulation of the **BB84 Quantum Key Distribution (QKD) protocol**. It allows you to visualize and understand the fundamental principles of quantum cryptography, including how Alice and Bob establish a shared secret key and how an eavesdropper (Eve) might compromise their communication.

The simulation uses `Qiskit` to mimic quantum operations like qubit encoding and measurement, providing a hands-on way to explore this important concept in quantum computing.

---

## Features

* **BB84 Protocol Simulation:** Implements the core steps of the BB84 protocol:
    * Alice prepares qubits with random bits and random bases (rectilinear or diagonal).
    * Bob measures qubits with random bases.
    * Sifting process where Alice and Bob compare their bases to distill a shared key.
* **Eavesdropping Simulation:** Introduces an optional eavesdropper (Eve) who intercepts and measures a percentage of the transmitted qubits. Eve's presence introduces detectable errors in the sifted key.
* **Detailed Visualization:** Generates a series of plots and a comprehensive summary table to clearly illustrate:
    * Alice's initial bits and bases.
    * Alice's and Bob's chosen bases.
    * Bob's measurement results.
    * Which bits were eavesdropped.
    * The final sifted key.
    * The calculated error rate in the sifted key, indicating potential eavesdropping.
* **Interactive Input:** Allows users to define the number of bits for key generation and the eavesdropping rate.

---

## How it Works (BB84 Protocol Explained)

The BB84 protocol relies on the principles of quantum mechanics to ensure secure communication. Here's a simplified breakdown of the steps simulated:

1.  **Alice Prepares Qubits:** Alice chooses a random bit (0 or 1) and a random measurement basis (Rectilinear `+` or Diagonal `X`) for each qubit. She then encodes the bit into the qubit using her chosen basis.
    * Rectilinear Basis: 0 is encoded as $|0\rangle$, 1 as $|1\rangle$.
    * Diagonal Basis: 0 is encoded as $|+\rangle$, 1 as $|-\rangle$.
    She sends these qubits to Bob.

2.  **Bob Measures Qubits:** For each incoming qubit, Bob randomly chooses one of the two measurement bases (Rectilinear `+` or Diagonal `X`) and measures the qubit.

3.  **Basis Comparison (Sifting):** Alice and Bob publicly communicate which bases they used for each qubit, but **not** the measurement results. They discard any qubits where their bases didn't match. For the qubits where their bases matched, their measurement results *should* be identical, forming the raw key.

4.  **Eavesdropping Detection:** If an eavesdropper (Eve) intercepts a qubit, she must also choose a random basis to measure it. If Eve chooses the wrong basis, she'll disturb the qubit's state, introducing errors that Alice and Bob can detect during public discussion of a small sample of their shared key. A high error rate signals the presence of an eavesdropper.

---

## Installation

To run this simulation, you'll need Python and the Qiskit library.

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/BB84-QKD-Simulator.git](https://github.com/your-username/BB84-QKD-Simulator.git)
    cd BB84-QKD-Simulator
    ```
2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

    **`requirements.txt` content:**

    ```
    numpy
    matplotlib
    qiskit
    qiskit-aer
    ```

---

## Usage

1.  **Run the Python script:**
    ```bash
    python bb84_simulator.py
    ```
    (Replace `bb84_simulator.py` with the actual name of your Python file if it's different).

2.  **Follow the prompts:**
    * Enter the **number of bits** for the key generation.
    * Enter the **eavesdropping rate** (a value between 0 and 1, where 0 means no eavesdropping and 1 means all bits are eavesdropped).
    * You will then be prompted to **enter each bit** (0 or 1) that Alice wants to send.

3.  **Analyze the output:**
    The script will display several plots visualizing the key generation process and a summary table. It will also print the final Alice's bits, chosen bases, Bob's results, the sifted key, and the calculated error rate. If the error rate is high enough (defaulting to >= 0.25), it will indicate that the "Communication Compromised!"

---

## Code Structure

* `generate_random_bases(n)`: Generates an array of random binary bases (0 for rectilinear, 1 for diagonal).
* `encode_qubits(bits, bases)`: Creates a `QuantumCircuit` to encode Alice's bits into qubits based on her chosen bases.
* `measure_qubits(qc, bases)`: Adds measurement operations to the quantum circuit, applying a Hadamard gate before measurement if the basis is diagonal.
* `simulate_eavesdropping(alice_bits, alice_bases, bob_bases, eavesdrop_rate)`: Simulates Eve's interception, including her random measurements and potential tampering of the bits if her basis choice differs from Alice's.
* `visualize_key_generation(...)`: Uses `matplotlib` to generate a multi-subplot visualization and a summary table of the entire QKD process.
* **Main Execution Block (`if __name__ == "__main__":`)**: Orchestrates the simulation, takes user input, calls the respective functions, runs the Qiskit simulation, and presents the results.

---

## Contributing

Feel free to fork this repository, open issues, or submit pull requests. Any contributions to enhance the simulation, add more features, or improve the visualizations are welcome!

---

## License

This project is open-source and available under the [MIT License](LICENSE).

---
