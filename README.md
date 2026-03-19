### Quick Study Plan for ROIC Concepts (Wednesday to Monday)

You've got ~5 days (Wed-Sun) to grasp the essentials: IRFPA/ROIC architecture, signal flow (photocurrent → integration → readout → digital output), key circuits (e.g., CTIA pixel, column amps, CDS), noise/biasing, and digital control basics. This builds intuition for your Verilog work starting Monday—focus on how digital timing/syncs with analog (e.g., reset/integration phases, row scanning). Aim for 3-5 hours/day: 20% reading, 80% sketching/diagramming/simulating (use free LTSpice for analog, ModelSim for digital if available; otherwise, paper sketches).

Prioritize **visual learning**: Draw block diagrams of signal flow, pixel schematics, and timing waveforms. Key concepts to master:
- **IRFPA Overview**: Hybrid detector-ROIC (bump-bonding), 2D array (e.g., 640x512), photocurrent input.
- **Pixel Circuits**: CTIA (capacitive transimpedance amp) for current-to-voltage integration; variants like direct-injection; integration capacitor, reset switches.
- **Readout Path**: Row-select, column buses, amps, CDS (noise reduction), sample-and-hold, multiplexing, ADC (shared or column-parallel).
- **Noise/Biasing**: Low-current handling, kTC/1/f noise, fixed-pattern noise cancellation.
- **Digital Control**: Row decoders, timing generators (FSMs for integrate/read), column scanning, frame output—prep for Verilog.
- **Overall Flow**: Analog front-end (pixel/column) → mixed-signal (ADC) → digital backend.

Ignore detector physics/fabrication—stick to ROIC.

#### Day-by-Day Order & What to Study
1. **Wednesday (Today: Overviews & Signal Flow, 3-4 Hours)**  
   Goal: High-level architecture intuition.  
   - Study: IRFPA system, hybrid integration, overall ROIC block diagram/signal path.  
   - Read: "Focal-Plane-Arrays and CMOS Readout Techniques of Infrared Imaging Systems" by Chih-Cheng Hsieh et al. (you have; focus Sections I-III for basics, ~1 hour). Then skim "ROIC Architectures and Strategies for Uncooled Micro-Bolometers IRFPA: A Review" by Samuele Fusetto et al. (you have; Sections 1-2 for architectures, ~1 hour).  
   - Do: Sketch full signal flow (detector → pixel → column → ADC → digital). Note digital-analog interfaces (e.g., row-select signals).  
   - Output: 1-page summary diagram for mentor.

2. **Thursday (Pixel Circuits & Analog Front-End, 4 Hours)**  
   Goal: Understand core analog blocks.  
   - Study: Pixel unit cells (CTIA focus: how photocurrent integrates on cap, reset mechanisms), biasing for low currents.  
   - Read: "The Design of a Low-Noise, High-Speed ROIC for IRFPA" by Yusong Mu et al. (you have; focus pixel sections & diagrams, ~1.5 hours). Cross with "Low-Power Low-Noise CTIA ROIC Design for Thermal Imaging Applications" by M. Rafat M. et al. (you have; CTIA specifics, ~1 hour).  
   - Do: Draw/simulate simple CTIA circuit (input current → amp → cap → output voltage). Vary params (e.g., cap size for gain).  
   - Output: Notes on pixel trade-offs (noise vs. speed).

3. **Friday (Column Readout & Noise Reduction, 4 Hours)**  
   Goal: Mid-chain processing.  
   - Study: Column amps, CDS (correlated double sampling for noise), sample-and-hold, multiplexing to ADC.  
   - Read: Continue Mu et al. (column/ADC parts) + "A High-Precision and High-Linearity ROIC for IRFPA Applications" by Tong Zhou et al. (you have; linearity/noise focus, ~2 hours total). Skim Vampola's "Readout Electronics for IR Sensors" Chapter 5 (you have; noise sections, ~1 hour).  
   - Do: Diagram readout sequence (row scan → column bus → CDS → mux). Simulate CDS (reset sample vs. signal sample).  
   - Output: Noise mitigation summary.

4. **Saturday (Digital Control & Mixed-Signal Integration, 4 Hours)**  
   Goal: Tie to Verilog—focus on digital's role.  
   - Study: Row/column decoders, timing FSMs, frame controllers, ADC syncing.  
   - Read: "Digital ROIC Implementing Time Delay and Integration (TDI) for Scanning Type IRFPA" by Omer Ceylan et al. (you have; digital blocks/TDI as scanning example, ~2 hours). Skim Khoshakhlagh's UNM Thesis (you have; Ch. 2-3 for mixed-signal, ~1 hour—excerpt digitally if long).  
   - Do: Sketch Verilog-like FSM (states: integrate, reset, read) + counters for scanning. Note how digital triggers analog (e.g., reset switch).  
   - Output: Digital-analog interface notes.

5. **Sunday (Review & Synthesis, 3 Hours)**  
   Goal: Consolidate for Monday report.  
   - Study: Full game plan recap—simulate small array flow if time.  
   - Read: Quick re-skim Hsieh + Mu for cohesion. Use Daniels' "Field Guide to IR Systems" book (you have; quick lookups on ROIC sections, no full read).  
   - Do: Compile 2-3 page report: Diagrams, key concepts, questions for mentor (e.g., specific sim tools). Practice explaining signal flow verbally.  
   - Output: Polished report/slides.

#### Must-Have Things to Print (Limited to ~50 Pages Total)
Print only essentials: Diagrams, schematics, key sections—focus on visuals for quick reference. From your downloads, prioritize short papers (no full books/thesis—excerpt if needed). Get these printed today:
1. **Hsieh et al. (1997)**: Full ~12 pages (overviews, block diagrams).
2. **Mu et al. (2023)**: Full ~18 pages (pixel/CTIA schematics, readout flow).
3. **Tong Zhou et al. (2019)**: Full ~8 pages (precision circuits, noise).
4. **Ceylan et al. (2016)**: Sections 3-5 ~10 pages (digital scanning/TDI for Verilog prep).
5. **Fusetto et al. Review**: Sections 2-4 ~10 pages (architectures, strategies).

This keeps you focused—report confidently on Monday, then pivot to Verilog with solid context. If overwhelmed, simplify: One diagram per concept. Good luck!

ROIC PPT Content
---

# 🎤 Slide 1 — Title

*(Based on page 1 )*

“Good morning, I’m Devansh.
In this presentation, I’ll walk through the fundamentals of infrared imaging and focus on how CMOS ROIC architectures have evolved to efficiently read very small IR signals.
This is based on my study of key papers and textbooks in this domain.”

---

# 🎤 Slide 2 — Infrared Radiation

“Let’s start with the basics — infrared radiation.
IR lies just beyond visible light in the electromagnetic spectrum and is primarily associated with heat.
Any object above absolute zero emits IR radiation, and the intensity increases with temperature.

Different wavelength bands like SWIR, MWIR, and LWIR are used for different applications, depending on temperature range and sensing requirements.”

---

# 🎤 Slide 3 — Thermal Radiation Laws

“To understand IR imaging, we need some fundamental physics.

Stefan–Boltzmann law tells us that emitted power increases with the fourth power of temperature, so even small temperature changes matter.
Wien’s law tells us that hotter objects emit at shorter wavelengths.

Together, these explain why different IR bands are used for different temperature ranges.
Blackbody radiation gives us the ideal reference for emission.”

---

# 🎤 Slide 4 — Emission vs Reflection

“In real-world scenarios, objects are not perfect emitters.

Emissivity defines how efficiently an object emits radiation.
Some objects emit strongly, like humans, while others reflect IR, like polished metals.

This distinction is important because reflected IR does not represent the object’s temperature.

Also, MWIR is more useful for hot targets, while LWIR is used for ambient temperature imaging.”

---

# 🎤 Slide 5 — IR Imaging System (Hybrid Structure)

“This is the core hardware structure.

Modern IR cameras use a two-chip hybrid system:
a detector array on top and a CMOS ROIC below, connected using indium bump bonding.

The detector materials like HgCdTe and InSb convert IR into electrical signals.
HgCdTe is tunable across bands, while InSb is very sensitive in MWIR.

There are also two types of detectors:
photon detectors, which generate charge directly, and thermal detectors like bolometers, which rely on temperature change.

The ROIC then processes this very weak signal.”

---

# 🎤 Slide 6 — ROIC Functions

“This slide shows what the ROIC actually does.

It starts at the pixel level, where the signal is acquired and integrated.
Then it is sampled, multiplexed across rows and columns, and processed in the analog domain.

Finally, it is converted to digital using ADC and sent out.

So essentially, ROIC acts as the interface that converts raw detector signals into usable digital image data.”

---

# 🎤 Slide 7 — Design Parameters

“Now, the design of ROIC is driven by several key parameters.

Detector bias stability is critical for linearity.
Injection efficiency determines how much signal is actually captured.
Noise affects the minimum detectable signal.

And all of this must be balanced with pixel area and power consumption.

These constraints drive the evolution of different architectures.”

---

# 🎤 Slide 8 — Self Integration

“We start with the simplest method — self-integration.

Here, charge directly accumulates at the detector node without any active circuitry.
This makes it very simple and low power.

But the problem is that the detector bias changes during integration, leading to nonlinearity and high noise.

So better control is needed.”

---

# 🎤 Slide 9 — SFD

“To improve this, SFD introduces a source follower buffer.

It helps in reading out the voltage without heavily loading the detector.

However, the charge is still stored at the detector node, so bias variation and noise issues remain.

This motivates moving the integration away from the detector.”

---

# 🎤 Slide 10 — DI

“Direct Injection is the first major improvement.

Here, photocurrent is directly injected into an integration capacitor through a common-gate transistor.
This keeps the detector bias more stable.

However, not all current is captured — injection efficiency is less than one, especially at low signal levels.

So performance drops in low-light conditions.”

---

# 🎤 Slide 11 — GMI & BDI

“To address DI limitations, improved architectures were developed.

GMI uses gate modulation and current mirrors to amplify the signal before integration.
BDI introduces feedback using an amplifier to reduce input impedance.

This significantly improves injection efficiency and sensitivity.

So we move from passive control to active control.”

---

# 🎤 Slide 12 — CTIA

“CTIA is the most advanced and widely used architecture.

It uses a high-gain amplifier with feedback to keep the detector node at constant voltage, also called virtual ground.

This ensures nearly perfect injection efficiency and excellent linearity.

However, it comes at the cost of higher power and larger pixel area.

So it’s a trade-off between performance and complexity.”
---

Questions : 
---
Great — this is where you can really stand out. I’ll give you **realistic jury questions + crisp answers**, not textbook ones.

---

# 🎯 🔥 Core Concept Questions

---

### ❓ 1. Why do we even need ROIC? Why not directly read detector output?

👉 **Answer:**
IR detectors generate **extremely small currents (pA–nA range)**.
These signals are:

* noisy
* high impedance
* not directly usable

ROIC is required to:

* bias the detector properly
* integrate and amplify signal
* convert it into usable voltage/digital output

---

### ❓ 2. Why is detector bias stability important?

👉 **Answer:**
Detector characteristics depend strongly on bias voltage.
If bias changes:

* responsivity changes
* nonlinearity increases

So keeping **constant bias ensures linear and accurate sensing**.

---

### ❓ 3. What is injection efficiency and why is it important?

👉 **Answer:**
[
\eta = \frac{I_{integrated}}{I_{photocurrent}}
]

It tells how much of detector current is actually captured.

* Low η → signal loss
* High η → better sensitivity

DI suffers at low current because η drops.

---

### ❓ 4. Why does DI fail at low photocurrent?

👉 **Answer:**
At low current:

* MOSFET input impedance increases
* More current leaks through detector

So less current reaches integration capacitor → poor sensitivity.

---

### ❓ 5. Why is CTIA considered best?

👉 **Answer:**

* Keeps detector voltage constant (virtual ground)
* Nearly **100% injection efficiency**
* High linearity

But trade-offs:

* higher power
* larger area

---

# ⚙️ Circuit-Level Questions

---

### ❓ 6. Why common-gate configuration is used in DI?

👉 **Answer:**
Common-gate provides:

* low input impedance
* fast current transfer

This helps in directly injecting photocurrent into capacitor.

---

### ❓ 7. Why PMOS is used instead of NMOS in DI?

👉 **Answer:**

* Better compatibility with detector bias levels
* Lower 1/f noise
* Easier integration in IRFPA process

---

### ❓ 8. What is virtual ground in CTIA?

👉 **Answer:**
Input node is held at constant voltage due to high-gain feedback.
Even though current flows, voltage doesn’t change.

---

# 🔬 Detector + System Questions

---

### ❓ 9. Difference between photon and thermal detectors?

👉 **Answer:**

| Photon                     | Thermal                   |
| -------------------------- | ------------------------- |
| Generate carriers directly | Detect temperature change |
| Fast, high sensitivity     | Slower                    |
| Require cooling            | Operate at room temp      |

Examples:

* Photon → HgCdTe, InSb
* Thermal → Bolometer

---

### ❓ 10. Why HgCdTe is widely used?

👉 **Answer:**

* Tunable bandgap → can detect SWIR to LWIR
* High quantum efficiency

---

### ❓ 11. Why cooling is required in IR detectors?

👉 **Answer:**
To reduce:

* dark current
* thermal noise

This improves signal-to-noise ratio.

---

# 🧠 System/Architecture Questions

---

### ❓ 12. Why hybrid architecture (detector + ROIC)?

👉 **Answer:**

* Detector materials ≠ CMOS compatible
* ROIC needs CMOS

So:
👉 best detector + best electronics separately → connected via bump bonding

---

### ❓ 13. What are main noise sources in ROIC?

👉 **Answer:**

* Thermal noise
* 1/f noise
* Reset noise (KTC)

---

### ❓ 14. What is KTC noise?

👉 **Answer:**
Noise introduced during capacitor reset:
[
V_n = \sqrt{\frac{kT}{C}}
]

---

### ❓ 15. Trade-offs in ROIC design?

👉 **Answer:**

* Performance vs power
* Sensitivity vs pixel size
* Noise vs speed

---

# 🔥 Smart / Analytical Questions

---

### ❓ 16. If you had to choose between DI and CTIA, what would you choose?

👉 **Answer:**

* For high-performance → CTIA
* For low-power / compact → DI

Depends on application requirements.

---

### ❓ 17. What drives evolution of ROIC architectures?

👉 **Answer:**
Improving:

* injection efficiency
* detector bias stability
* noise performance

---

### ❓ 18. Can digital ROIC replace analog ROIC?

👉 **Answer:**
Not fully.
Analog front-end is still required because:

* signal is extremely small
* must be conditioned before digitization

---

# 🎯 Final tip (VERY IMPORTANT)

If you don’t know an answer:

👉 Say:

> “I haven’t explored that in detail yet, but based on my understanding…”

Then connect it to what you know.

---

# 🧠 Most likely questions for YOU specifically

From your PPT, expect:

* DI vs CTIA difference
* Injection efficiency
* Why PMOS
* Hybrid structure
* Photon vs thermal detectors
