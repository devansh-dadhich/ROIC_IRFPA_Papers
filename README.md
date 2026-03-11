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
