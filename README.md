# Zero-to-Silicon — Event 1 — Open Neuromorphic

 <div align="center">
  <img src="https://em-content.zobj.net/source/microsoft-teams/400/brain_1f9e0.png" style="width:16%">
</div>

<div align="center">
  <h2> Event 1 — Neuroscience foundations for neuromorphic computation </h2>
  <h6>The purpose of this material is to understand the minimal biological principles that make event-driven neural computation possible, focusing on dynamic systems. And yes, the pulsing brain emoji also hurts my eyes.</h6>
</div>

### Overview
<h4>Description</h4
<p>
This tutorial aims at building intuition for how biological neural computation informs neuromorphic design. Move from mechanism to abstraction, always asking: what must be preserved, and what can be simplified?
</p>

<h4>Target</h4>
<p>
  Engineers, computer scientists, or researchers and students entering neuromorphic computing with basic programming background but limited neuroscience exposure.
</p>



<table>
  <thead>
    <tr>
      <th>Module</th>
      <th>Guiding questions</th>
      <th>Core concepts</th>
      <th>Models used</th>
      <th>Demo</th>
      <th>Challenge</th>
      <th>Neuromorphic bridge</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1. What is a neuron?</td>
      <td>What type of dynamical system is a neuron?</td>
      <td>Basic morphology, membrane potential, spike as discrete event, input → integration → output</td>
      <td>Conceptual</td>
      <td>Patch clamp: voltage trace under input current</td>
      <td>-</td>
      <td>Event-driven state transitions</td>
    </tr>
    <tr>
      <td>2. Excitable membranes</td>
      <td>Under what conditions does a neuron generate a spike?</td>
      <td>Leakage, integration, threshold, refractory period</td>
      <td>Leaky integrate-and-fire (LIF)</td>
      <td>Current injection; vary threshold and time constant</td>
      <td>Analyze effect of removing leak</td>
      <td>Minimal spike-based computation</td>
    </tr>
    <tr>
      <td>3. Biophysical spike generation</td>
      <td>What mechanisms produce the action potential?</td>
      <td>Voltage-gated Na⁺ activation, K⁺ recovery, feedback dynamics</td>
      <td>Hodgkin–Huxley</td>
      <td>Inspect gating variables (m, h, n); vary conductances</td>
      <td>Induce hyperexcitability; compare to LIF approximation</td>
      <td>Biologically grounded simplification</td>
    </tr>
    <tr>
      <td>4. Synaptic communication</td>
      <td>How does one neuron affect another?</td>
      <td>Synaptic currents, weights, temporal summation, coincidence detection</td>
      <td>LIF or HH with synapses</td>
      <td>Presynaptic spike trigger; adjust weight and delay</td>
      <td>Determine minimal synaptic weight for postsynaptic firing</td>
      <td>Weighted event transmission</td>
    </tr>
    <tr>
      <td>5. Excitation and inhibition</td>
      <td>How is network activity stabilized?</td>
      <td>E/I balance, feedback, gain control, oscillatory regimes</td>
      <td>Small excitatory–inhibitory network</td>
      <td>Design an E/I network that maintains activity within a target firing rate range</td>
      <td>Characterize stable vs unstable parameter regimes</td>
      <td>Stability constraints in hardware</td>
    </tr>
    <tr>
      <td>6. Structure and compartmentalization</td>
      <td>Does spatial structure alter integration?</td>
      <td>Dendritic compartments, nonlinear summation, spatial separation</td>
      <td>Two-compartment pyramidal model</td>
      <td>Compare somatic vs dendritic input effects</td>
      <td>Demonstrate nonlinear amplification of distal input</td>
      <td>When spatial modeling matters</td>
    </tr>
    <tr>
      <td>7. Abstraction for neuromorphic systems</td>
      <td>Which biological mechanisms must be preserved?</td>
      <td>Model reduction, sparsity, event-based signaling, energy constraints</td>
      <td>HH vs LIF comparison</td>
      <td>Side-by-side dynamical comparison</td>
      <td>Design a reduced neuron preserving coincidence detection and stability</td>
      <td>Principled abstraction for hardware</td>
    </tr>
  </tbody>
</table>


<h6>
  <details>
  <summary>References</summary>
  <div>
    "Principles of Neural Science (5th ed.)" McGraw-Hill Education. Retrieved from https://www.mhprofessional.com/principles-of-neural-science-fifth-edition-9780071390118-usa
   <br>
    "Neuronal Dynamics: From Single Neurons to Networks and Models of Cognition" Cambridge University Press. Retrieved from https://neuronaldynamics.epfl.ch/online/index.html
  </div>
  </details>
</h6>

---
# 🇲 1️⃣ What is a neuron?

# 🇲 2️⃣ Excitable membranes

# 🇲 3️⃣ Biophysical spike generation

