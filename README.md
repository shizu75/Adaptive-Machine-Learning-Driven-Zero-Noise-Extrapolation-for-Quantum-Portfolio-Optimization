# Adaptive Machine Learning–Driven Zero-Noise Extrapolation for Quantum Portfolio Optimization

## Abstract

This repository presents a **research-oriented implementation of adaptive Zero-Noise Extrapolation (ZNE)** enhanced by **deep learning**, applied to **quantum approximate optimization algorithms (QAOA)** for portfolio optimization. The work bridges **quantum error mitigation**, **statistical finance**, and **machine learning**, demonstrating how learned noise-scaling strategies can outperform static extrapolation in noisy quantum simulations.

The implementation is fully **Python 3.12 compatible**, leverages **real financial market data**, and follows **methodological rigor aligned with contemporary quantum computing research**. All components—from data acquisition to quantum circuit execution and error analysis—are implemented from first principles.

---

## Research Motivation

Noisy Intermediate-Scale Quantum (NISQ) devices suffer from stochastic and systematic errors that significantly degrade algorithmic performance. **Zero-Noise Extrapolation** is one of the most hardware-agnostic mitigation strategies, but classical implementations rely on **fixed, heuristic noise scaling schedules**.

This work proposes and evaluates an **ML-guided ZNE framework** in which a **CNN–LSTM model dynamically predicts optimal noise-scaling factors**, enabling adaptive extrapolation under changing noise conditions. The framework is evaluated on a **QAOA-based formulation of mean–variance portfolio optimization**, providing both algorithmic and application-level validation.

---

## System Overview

The pipeline consists of six tightly integrated stages:

1. **Financial Data Acquisition**
2. **QUBO and Ising Model Construction**
3. **Quantum Circuit Design (QAOA)**
4. **Controlled Noise Injection**
5. **Static vs ML-Based Zero-Noise Extrapolation**
6. **Statistical and Visual Evaluation**

---

## Financial Modeling

- Data source: **Fama–French daily factor returns**
- Assets used: Market excess return (MKT-RF), SMB, HML
- Returns normalized to decimal form
- Mean return vector (μ) and covariance matrix (Σ) computed empirically
- Portfolio optimization expressed as a **QUBO problem**:
  - Risk-adjusted objective with tunable risk-aversion parameter
  - Converted analytically into an **Ising Hamiltonian**

---

## Quantum Formulation

### QAOA Circuit
- Binary portfolio weights encoded as qubits
- Initial uniform superposition via Hadamard gates
- Cost Hamiltonian implemented using parameterized Z-rotations and CX entanglers
- Mixer Hamiltonian via RX rotations
- Measurement in the computational basis

### Noise Model
- Custom-built **depolarizing noise model**
- Independent control of:
  - Single-qubit gate noise
  - Two-qubit gate noise
- Noise scaling parameter λ ∈ [1, 3]
- Fully compatible with AerSimulator

---

## Zero-Noise Extrapolation Strategies

### Static ZNE
- Fixed noise scaling factors
- Linear extrapolation to the zero-noise limit
- Serves as the classical baseline

### Machine Learning–Based ZNE
- **CNN–LSTM neural network** predicts noise scaling factors
- Input: synthetic noise metrics representing calibration summaries
- Output: adaptive noise scaling values constrained to physically meaningful bounds
- Model trained end-to-end using supervised regression

---

## Machine Learning Architecture

- **1D Convolutional Layer** for feature extraction
- **LSTM Layer** for temporal dependency modeling
- Fully connected output layer with bounded activation
- Optimized using Adam optimizer and MSE loss
- Designed for fast inference during quantum circuit execution

---

## Evaluation Protocol

- Repeated calibration cycles to simulate temporal noise drift
- Comparison metrics:
  - Absolute extrapolation error
  - Signal-to-noise ratio (Sharpe-like metric)
- Parameter landscape analysis across β–γ grids
- Visual diagnostics for:
  - Noise scaling trajectories
  - Error convergence
  - Optimization surface smoothness

---

## Key Findings

- ML-ZNE exhibits **lower variance and improved stability** compared to static ZNE
- Adaptive scaling better tracks simulated noise fluctuations
- Improved signal-to-noise ratios across repeated trials
- Smoother and more coherent optimization landscapes under ML-based mitigation
- Demonstrates feasibility of **learning-assisted error mitigation** in variational quantum algorithms

---

## Scientific Significance

This work illustrates that **error mitigation itself can be treated as a learning problem**, rather than a fixed analytical correction. By embedding machine learning directly into the quantum execution loop, the framework adapts to noise statistics in real time, offering a scalable and backend-agnostic pathway toward improved NISQ performance.

The methodology generalizes naturally to:
- Other variational algorithms
- Alternative cost Hamiltonians
- Real hardware execution with live calibration data

---

## Reproducibility and Environment

- Fully deterministic pipeline (random seeds controlled where applicable)
- Uses only open datasets and open-source libraries
- Compatible with Python 3.12
- Explicit dependency versions specified
- Designed for local simulation and cloud-based quantum backends

---

## Keywords

Quantum Error Mitigation, Zero-Noise Extrapolation, Machine Learning, CNN-LSTM, QAOA, Quantum Finance, NISQ Algorithms, Portfolio Optimization, Hybrid Quantum-Classical Systems
