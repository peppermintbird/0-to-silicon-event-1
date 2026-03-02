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
**Guiding question:** What type of dynamical system is a neuron? We will come back to this question soon.

## The biological story
A neuron, conceptually, is a decision-making device that lives in time. It constantly receives small signals from other neurons. Each of those signals nudges its internal state up or down. That internal state doesn’t stay fixed — it naturally drifts back toward rest if nothing happens. So the neuron is always balancing incoming influence against its own tendency to relax. If enough input accumulates fast enough, the neuron crosses a critical point and emits a spike — a brief, stereotyped pulse. After that, it resets and the process starts again. 

### Neuron as an electrical device
In other words, neurons receive **voltages** as **synaptic inputs** from other neurons that can rapidly change the electrical internal state of the neuron or **membrane potential**. However, at same time, neurons will have a pull toward **resting potential** that sits around -70 mV provoked by the leak conductance. This way, inside the neuron, this voltage is constantly being pushed and pulled by inputs from other neurons. Until at a certain point, when input is enough, the voltage reaches a critical point, the **threshold**. After crossing it, there's a spike or **action potential**. And the neuron returns to rest potential once again. So, you understand the narrative, but what system is there?

Phase 1. **Integration:** The membrane potential rises gradually as charge accumulates;

Phase 2. **Threshold crossing:** When voltage reaches ~-55 mV, the neuron suddenly "fires";

Phase 3. **Spike generation:** A stereotyped electrical pulse (action potential) shoots down the axon;

Phase 4. **Reset:** The neuron returns to rest and briefly becomes unresponsive (refractory period).

From the outside, the neuron either fires or it doesn’t with the same spike every time. So, it it just a binary device flipping on and off? Let's delve deeper into that.

### The all-or-nothing principle

Here's what makes neurons fundamentally different from analog electronics: **the spike amplitude doesn't encode information**. 

Whether you barely cross threshold or massively exceed it, the spike looks the same, which translates to roughly +40 mV, lasting ~1-2 milliseconds. 

```
[insert] graph of weak input vs strong input
```

This is an "Aha!" moment: strong inputs will generate more frequent spikes. This is the neuron's digital moment, the spike is a standardized signal, like a packet on a network.

---

## What information does the spike carry?


---

## The demo

➡️ [NeuronBench patch-clamp simulator](https://nbnch.io/s/xnzs-qhdf)

---

## The challenge
For your first challenge, you will play with the parameters of the patch-clamp simulator introduced in the demo. However, now follow the instructions and answer the questions.

➡️ [NeuronBench patch-clamp simulator](https://nbnch.io/s/xnzs-qhdf)

### Part 1: find the threshold
- Start with small Onset Current values (try 0.1 µA, 0.2 µA, 0.3 µA...)
- Set Period = 100 ms, Onset Time = 20 ms, Offset Time = 80 ms
- What's the minimum current that produces a spike?

### Part 2: test spike invariance
- Set Onset Current to **just above threshold** (e.g., if threshold is ~0.3 µA, use 0.35 µA)
- Measure the peak voltage of the spike
- Now double the Onset Current (e.g., 0.7 µA)
- Measure the spike amplitude again
- Did the spike get twice as tall? Or did something else change?

### Part 3: explain
**Why does spike amplitude stay constant while spike count increases with input strength?**

---

## 🌉 Neuromorphic bridge: event-driven state transitions

Traditional computers (and artificial neural networks) use **continuous-valued activations**:
```
neuron_output = sigmoid(weighted_sum_of_inputs)  # continuous value 0-1
```
<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/c2f20024-b2b2-46f2-8011-8425c040c84d" />

But biological neurons use **discrete events**:
```
if membrane_potential >= threshold:
    emit_spike()  # binary event
    reset()
```
<img width="500" height="136" alt="image" src="https://github.com/user-attachments/assets/8a715401-2704-457b-ba84-53c7b1db7429" />

This is the foundation of event-driven computation.

### Why does this matter for neuromorphic systems?

**1. Sparsity**  
Most neurons are silent most of the time. In the brain, ~1% of neurons are active at any moment. If you only compute when events happen (spikes), you can power down 99% of your hardware.

**2. Asynchrony**  
Spikes don't happen on a clock cycle. Neuron A might fire at t=3.7 ms, neuron B at t=8.2 ms. This asynchronous operation means no global synchronization overhead.

**3. Communication Efficiency**  
Sending a spike is just an address and a timestamp: "Neuron 4729 fired at t=15.3 ms." Compare this to sending continuous 32-bit floating-point values every timestep.

**4. Temporal Precision**  
Information is in the *timing* of events, not just their presence. A 1 ms difference in spike arrival can determine whether a downstream neuron fires. This enables computation based on coincidence detection and precise temporal patterns.

### The computational paradigm shift

| Traditional computing | Event-driven (Neuromorphic) |
|-----------------------|-----------------------------|
| Clock-driven, synchronous | Asynchronous, event-triggered |
| Continuous values | Discrete events |
| Compute every cycle | Compute only when input arrives |
| High power (always active) | Low power (sparse activity) |
| Time is implicit (clock ticks) | Time is explicit (spike timing) |


# 🇲 2️⃣ Excitable membranes

# 🇲 3️⃣ Biophysical spike generation


