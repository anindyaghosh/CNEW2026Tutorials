
# NPC Lab for the Event-Driven Vision School 2026 

<p align="center">
  <img src="images/NPClab.png" alt="NPC Lab Logo" width="600"/>
</p>

### Neuro-inspired Perception and Cognition (NPC) Lab — Czech Technical University in Prague

This tutorial series is part of the teaching activities of the [**Neuroinspired Perception and Cognition (NPC) Lab**](https://giuliadangelo.github.io/html/npclab.html) at the 
**Department of Cybernetics, Faculty of Electrical Engineering, Czech Technical University 
in Prague**, led by [Assistant Professor Giulia D'Angelo](https://www.giuliadangelo.com/). 
It introduces students to the computational principles of spiking neurons, 
the fundamental building blocks of neuromorphic computing and brain-inspired 
artificial intelligence.

These tutorials are designed and developed by the NPC Lab team: 
- Giulia D'Angelo (giulia.dangelo@fel.cvut.cz)  (Principal Investigator)
- Sarka Liskova (sarka.liskova@fel.cvut.cz) (PhD student)
- Paolo Ritirato (paolo.ritirato@fel.cvut.cz) (PhD student)
- Olha Vedmedenko (vedmeolh@fit.cvut.cz) (Bachelor Student)
- Rayane Rocha (rayane.rocha@cvut.cz) (Bachelor Student)
- Lukáš Bartůněk (bartulu2@fel.cvut.cz) (Master Student)


## 2026 CNEW TUTORIALS

For more tutorials on event-driven sensing and neuromorphic computing, visit:

[github.com/GiuliaDAngelo/CTU-EDNeuromorphic](https://github.com/GiuliaDAngelo/CTU-EDNeuromorphic)

## Tutorial — Object Motion Sensitivity (OMS)

**Script:** [`Tutorial-OMS.py`](https://github.com/Neuro-inspired-Perception-and-Cognition/EVSchool2026/blob/main/Tutorial4-OMS.py)

This tutorial implements an **Object Motion Sensitivity (OMS)** network,
a biologically inspired mechanism for motion segmentation directly
derived from the research of the NPC Lab.
The system analyses event-based frames using
centre-surround spatial kernels to detect local motion differences,
producing a segmentation map comparable with ground-truth masks.

> **Key concept:** OMS cells are modelled on retinal
> amacrine cells that respond selectively to
> objects moving differently from their static background.
>
> This work is directly connected to [D'Angelo et al., 2025](https://doi.org/10.1088/2634-4386/addc90).

**Download data:** [Dropbox link](https://www.dropbox.com/scl/fo/g5j17yh6elrc61s66aiba/AO2lSvWa5oLlZYhc0V2CNkw?rlkey=w0hgpsbd2mjvbfp4vrtdm5bhe&st=hi09k9to&dl=0)

Place the data in `data/evimo/` before running the script.

### Exercises

**Task 1 — Explore the OMS threshold**

Run the script and observe the three panels: the input event frame, the ground-truth segmentation mask, and the OMS output. Then vary the `threshold` parameter in `OMS_PARAMS` and observe how the segmentation changes:

```python
OMS_PARAMS = {
    ...
    'threshold': 0.86,  # try values between 0.5 and 1.0
    ...
}
```

What happens when the threshold is very low? What happens when it is very high?

**Task 2 — Compute the OMS motion score**

For a randomly selected frame, compute the percentage of pixels classified as motion by the OMS network:

```python
frame_idx = np.random.randint(len(evframesdata))
threshold = config.OMS_PARAMS['threshold']

# TODO: compute the OMS output for the selected frame
# TODO: compute the percentage of motion pixels (OMS == 255)
motion_ratio = None

print(f"Frame index: {frame_idx}")
print(f"Motion ratio (%): {motion_ratio:.2f}")
```

**Task 3 — Explore OMS parameters**

Vary the parameters in `OMS_PARAMS` (kernel sizes, sigma values) and observe how segmentation quality changes. Which parameters have the most impact?

### Questions

1. How does the difference between centre and surround responses contribute to motion segmentation?
2. How does the choice of `threshold` affect the OMS output — what happens at very low or very high values?
3. Which `OMS_PARAMS` have the most impact on segmentation quality and why?
---

## Bonus — Live Demo: OMS on Neuromorphic Hardware

<p align="center">
  <img src="https://github.com/Neuro-inspired-Perception-and-Cognition/EVSchool2026/blob/main/images/demo.png" alt="NPC Lab Logo" width="200"/>
</p>

For a live demonstration of the OMS pipeline deployed on the
**SynSense Speck2f** neuromorphic chip, see the companion repository:

[github.com/GiuliaDAngelo/Speckegomotion](https://github.com/GiuliaDAngelo/Speckegomotion)

This demo is directly connected to [D'Angelo et al., 2025](https://doi.org/10.1088/2634-4386/addc90) and shows the full OMS, visual attention and control pipeline running in real time on neuromorphic hardware with event-based eye movements under two conditions:

- **Microsaccades** — small continuous jitter movements around a fixed position, producing a steady stream of events even in a static scene
- **Saccades** — large ballistic jumps to random positions, alternating between dense event bursts and complete silence

The two conditions reveal how eye movement strategy shapes the output of the OMS network on-chip.

---

*NPC Lab — Czech Technical University in Prague | Faculty of Electrical Engineering | Department of Cybernetics*
*Contact: [giulia.dangelo@fel.cvut.cz](mailto:giulia.dangelo@fel.cvut.cz)*

