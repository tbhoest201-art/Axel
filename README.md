# Identity Tube — Perturbation Sensitivity Screening in Dale-Compliant LIF Networks

**Status:** Toy computational model, not a biological brain or production AI system.  
**Seed for all figures:** 42 (Phase III-IV, VIII) / 7 (Phase I-II)

This repo implements the framework from biological_teleportation_research_roadmap.pdf Sections 6-9

## Quick Reproduce
python identity_tube_phase1_phase2.py
python identity_tube_phase3_hub_vs_peripheral.py
python identity_tube_phase4_degree_sensitivity.py

Outputs:
- identity_tube_micro_distance.png — D_S(t) decays to ~0 in 100 ms
- identity_tube_functional_distance.png — D_Y(t) ~0 Hz
- hub_vs_peripheral_DS.png / DY.png
- degree_vs_functional_sensitivity.png — degree vs peak D_Y, Pearson r = 0.556

## Core Finding (Phase VIII — degree-controlled)
31 nodes all degree 8, identical local degree.

- Node 77 (Strategic Amplifier): Peak D_Y 65.0 Hz, W1 +14.4, W2 +774.36, W3 +27,383.184
- Node 161 (Silent Resilient): Peak D_Y 0.5 Hz, W1 -32.0, W2 -1,468.8, W3 -46,319.04

Same degree, opposite signed trajectory. Total absolute magnitude does NOT predict sensitivity.
Ratio Node77 W3/W2 = 35.36

## Method
We present a computational framework for screening recurrent networks for perturbation-sensitive nodes by combining topology, signed directional connectivity, multi-hop propagation, and nonlinear dynamical response.

## Model Params
N=200, T=150 ms, DT=0.1 ms, TAU=20 ms, V_REST=-65, V_RESET=-70, V_THRESHOLD=-50
EXC_FRACTION=0.8, WEIGHT_EXC=1.8, WEIGHT_INH=-4.0, BASE_DRIVE=16.0
Scale-free m=8, row=presynaptic: weights[:n_exc,:]=EXC, weights[n_exc:,:]=INH
Perturbation: +1 mV single node

## Bug Fix Log
Original row/column weighting confusion. After enforcing Dale's Law correctly, Node 77 D_Y 55.5 Hz -> 65.0 Hz.

## Limitations — Must state in any outreach
- Demonstrated on 200-node LIF model, not a biological brain or production AI
- Original row/column weighting bug discovered and corrected
- W^k analysis is structural proxy; does not directly equal nonlinear neural activity
- Phase VIII result motivates but does not establish positive/negative propagation hypothesis
- Single seed (42), single topology, simplified synapses, no delays/adaptation/noise

## Next Validation — Phase IX
1. Split W^k into positive_mass and negative_mass per hop
2. Measure actual spike cascade duration after 1 mV
3. Test correlation positive_mass vs D_Y
4. Robustness: multiple seeds, N=200/500/1000, perturbations 0.1/1/5 mV
