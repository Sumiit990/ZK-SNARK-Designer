# ZK-SNARK-Designer

## Polygon zkSNARK Circuit Project

Welcome to the GitHub repository for the Polygon zkSNARK circuit project. This project involves designing a zkSNARK circuit that implements specific logical operations, compiling the circuit, generating proofs, and deploying an on-chain verifier to ensure the integrity and correctness of the proofs. This README outlines the project setup, usage, and the steps required to successfully deploy and test the zkSNARK verifier on the blockchain.

## Project Overview

You are tasked with creating a zkSNARK circuit using the `circom` language, compiling this circuit to generate necessary intermediaries, and then using these to generate a cryptographic proof. The project concludes with deploying a Solidity-based verifier on the Sepolia or Mumbai Testnet to validate proofs generated from your circuit.

### Tools Used

- **circom & snarkjs**: Used for writing, compiling the zkSNARK circuit, and generating proofs and the verifier.
- **Hardhat**: Utilized for deploying the verifier contract to the blockchain.
- **Hardhat-circom template**: This template helps streamline the development of zkSNARK projects within the Hardhat environment.

### Project Rubric

To successfully complete the project, you must:

1. **Write a Correct `circuit.circom` Implementation**: Your circuit should correctly implement the assigned logical operations.
2. **Compile the Circuit**: Generate the necessary circuit intermediaries, such as `witness`, `proof.json`, and `public.json`.
3. **Generate a Proof**: Using inputs `A=0` and `B=1`, generate a valid proof.
4. **Deploy a Solidity Verifier**: Deploy the verifier to either the Sepolia or Mumbai Testnet.
5. **Call the `verifyProof()` Method**: On the deployed verifier contract and assert that the output is `true`.

## Setup Instructions

### Prerequisites

Ensure you have Node.js and npm installed. Additionally, install the following globally:
```bash
npm install -g circom snarkjs
```

### Installation

Clone the repository and install dependencies:
```bash
git clone <repository-url>
cd <project-directory>
npm install
```

### Writing the Circuit

Create your zkSNARK circuit in `circuit.circom`. Refer to the `circom` documentation for syntax and logical components.

### Compiling the Circuit

Compile your circuit using the following commands:
```bash
circom circuit.circom --r1cs --wasm --sym
snarkjs r1cs info circuit.r1cs
```

### Generating the Proof

Generate a witness and proof using:
```bash
# Generate witness
snarkjs wtns calculate circuit.wasm input.json witness.wtns

# Generate proof and public parameters
snarkjs groth16 prove circuit_final.zkey witness.wtns proof.json public.json
```

### Deploying the Verifier

Deploy the verifier to the blockchain using Hardhat:
```bash
npx hardhat run scripts/deploy.js --network sepolia
```

### Testing the Verifier

Invoke the `verifyProof()` method and check the output:
```bash
npx hardhat run scripts/verify.js --network sepolia
```

## Support

If you encounter any issues or have questions, please open an issue in this repository or consult the documentation for the tools mentioned above.

## Conclusion

By completing this project, you will gain practical experience in zkSNARKs, an exciting area of blockchain development that enhances privacy and scalability. Your contribution pushes forward the capabilities of verifiable computations on the Polygon network. Good luck, and happy coding!
