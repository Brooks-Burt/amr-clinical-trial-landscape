# Did the Clinical Trial Pipeline Respond to the Global AMR Crisis?
 
> Evaluating whether research investment in antimicrobial resistance shifted following the 2015 WHO Global Action Plan — analyzed across 313 AMR-specific clinical trials from ClinicalTrials.gov.
 
<p>
  <a href="#executive-summary">Executive Summary</a> ·
  <a href="#business-problem">Business Problem</a> · 
  <a href="#methodology">Methodology</a> ·
  <a href="#skills">Skills</a> ·
  <a href="#results--business-recommendations">Findings</a> · 
  <a href="#summary-of-key-findings">Summary Table</a>
</p>

| 🧪 313 AMR Trials | 📈 236.6% Volume Growth | 💊 17x CRE Increase | 🏛️ Industry Sponsorship Declining |
|---|---|---|---|
| Identified from 1.17M registered studies | Post vs Pre WHO GAP 2015 | Most dramatic resistance shift | 38% → 35.6% post-WHO GAP |
 
**Tools:** PostgreSQL · Python · pandas · matplotlib · seaborn · Jupyter  
**Data:** [AACT — ClinicalTrials.gov](https://aact.ctti-clinicaltrials.org/) · 1.17M trials · Cohort: 313 AMR-specific trials  
**Author:** Brooks Burt · Computational Analysis, Infectious Disease · Broad Institute
 
---

## Executive Summary

Antimicrobial resistane is a growing concern in the world of biomedical research and medicine. Old antibiotics which were at one time deemed wonder drugs are no longer work as effectively as these pathogens are adapting and evolving to acquire resistance. 

In 2015, the World Health Organization published its Global Action Plan (WHO GAP) on Antimicrobial Resistance, establishing a coordinated international framework across five key objectives.

### WHO 5 objectives:
- to improve awareness and understanding of antimicrobial resistance;
- to strengthen knowledge through surveillance and research;
- to reduce the incidence of infection;
- to optimize the use of antimicrobial agents;
- develop the economic case for sustainable investment that takes account of the needs of all countries
and increase investment in new medicines, diagnostic tools, vaccines and other interventions.

This project asks the direct question **did the clinical trial pipeline actually respond?**

Analyzing 313 AMR-speciifc trials registered between 2004 and 2026, the data reveals a **236.6% increase in trial volume** following the 2015 WHO GAP - from 71 trials pre-2015 to 239 post-2015. Beyond raw volume, the data shows interesting and insightful shifts in pathogen focus, trial maturity, enrollment, and intervention strategy that suggests a genuine reserach response to the global AMR crisis. 

<img width="1155" height="572" alt="image" src="https://github.com/user-attachments/assets/5fe76db2-4c09-4d11-a81a-80b762a4f993" />


Critically, the analysis also surfaces a policy-relevant gap: **indsutry sponsorship declined slightly** from 38% to 35.6% post-WHO GAP, while academic and government institutions absorbed the growing trial burden. This raises important questions about the sustainability of AMR research and whether or not there will be a more delayed response by industry to this problem, or none at all. 

---

## Business Problem
 
Antimicrobial resistance represents one of the most complex challenges in modern medicine. The problem, AMR development is coincidentally one of the worst businesses in medicine. 
Effective antibiotics are used sparingly by design, prescribed for days rather than years, and often generically available, creating commercial returns that don't justify the billions spent on R&D.

The WHO GAP was designed in part to address this market failure by coordinating international policy, funding, and research prioritization.
 
**The core analytical question:** In the decade following the 2015 WHO Global Action Plan, did clinical trial activity reflect the five pillars of the framework?
 
This is examined across five dimensions:
 
- **Pillar 1 & 2 — Awareness & Knowledge:** Did trial volume and pathogen diversity increase?
- **Pillar 3 — Reduce Infection:** Did trial focus shift toward prevention and infection control?
- **Pillar 4 — Optimize Use:** Did trials targeting specific resistance mechanisms grow? Did combination therapy increase?
- **Pillar 5 — Sustainable Investment:** Did enrollment scale, late-stage trial rates, and industry engagement grow?

**Policy does not always reflect research reality. During this investigation, we will look into each pillar to see whether the research is responding.**

---

## Methodology
 
### Data Source
The AACT database provides a fully relational PostgreSQL snapshot of all ClinicalTrials.gov registrations, updated daily. The full static dump (~8GB) was restored locally and queried directly via PostgreSQL. All analysis was conducted in Python using pandas, matplotlib, and seaborn within Jupyter notebooks.

### Cohort Definition
Of 1,170,000+ registered trials in AACT, AMR-specific trials were identified using a dual-filter methodology requiring **both** of the following to be present in a trial's condition coding:
 
**Block 1 — Resistance terminology:**
- `-resistant`, `drug resistant`, `antimicrobial resistance`, `antibiotic resistance`
**Block 2 — Infectious pathogen context:**
- Specific organisms: *Staphylococcus*, *Tuberculosis*, *Klebsiella*, *Pseudomonas*, *Acinetobacter*, *Enterococcus*, *Enterobacteriaceae*, *Escherichia*, *Candida*, *Streptococcus*, *Campylobacter*, *Helicobacter*, *Gonorrhoeae*, *Salmonella*
- Broad context terms: `bacterial`, `antimicrobial`, `antibiotic`, `antifungal`, `infection`, `fungal`, `malaria`
This dual-filter approach was chosen to exclude non-AMR resistance conditions (oncological resistance, treatment-resistant depression, insulin resistance) that would otherwise inflate the cohort. A plain `%resistant%` filter returned 2,185 trials, the majority of which were unrelated to antimicrobial resistance.
 
Trials satisfying both blocks via an `EXISTS` subquery structure — requiring resistance and pathogen terms to be present at the trial level rather than within the same condition string — yielded a **final cohort of 313 trials**.

 ### Inflection Point
The WHO Global Action Plan on Antimicrobial Resistance (May 2015) was selected as the analytical inflection point, dividing the cohort into:
- **Pre-WHO GAP:** trials with start date before January 1, 2015 (n=71)
- **Post-WHO GAP:** trials with start date on or after January 1, 2015 (n=239)
- **Unknown:** trials with missing start dates excluded from period comparisons (n=3)


### Limitations
- Cohort size (313 trials) limits statistical power for subgroup analyses
- `drop_duplicates` on `nct_id` retains the first matching condition per trial; trials with multiple resistance mechanisms are therefore conservatively classified
- ClinicalTrials.gov registration is voluntary prior to 2017, meaning pre-2015 trial counts may be underrepresented
- The dataset includes prospectively registered trials with start dates through 2026

---
 
## Skills
 
| Area | Tools & Techniques |
|---|---|
| Database | PostgreSQL, AACT schema, complex JOIN and EXISTS subquery logic |
| Data Wrangling | Python, pandas, datetime parsing, outlier capping, deduplication |
| Analysis | Pre/post cohort comparison, sponsor classification, pathogen taxonomy |
| Visualization | matplotlib, seaborn, dual-axis charts, time series, grouped bar charts |
| Domain Knowledge | AMR biology, WHO GAP policy framework, clinical trial phases |
| Workflow | Jupyter notebooks, modular pipeline (EDA → Cleaning → Analysis) |
 
---

## Results & Business Recommendations
 
### Pillar 1 & 2 — Awareness & Knowledge
 
**Finding: Trial volume increased 236.6% post-WHO GAP**
The most direct signal of the WHO GAP's impact is the sheer increase in registered AMR trial activity. This growth is also very unlikely to be driven by registration behavior alone as mentioned earlier, the 2017 mandate would, if anything, mean that there was likely MORE trials PRE 2015 than reported. 

**Finding: Pathogen diversity expanded from 6 to 9 distinct pathogen groups**

<img width="2075" height="1026" alt="image" src="https://github.com/user-attachments/assets/5d3728db-a785-4d6f-8bb4-f7567e52accf" />

As AMR has become a greater priority, so too are the specific pathogens being studied. 

### Pillar 3 — Reduce Infection

<img width="1776" height="878" alt="image" src="https://github.com/user-attachments/assets/219a0383-2132-43c4-9eb6-a27b8f50b144" />


 | Intervention Type | Pre-WHO GAP | Post-WHO GAP |
|---|---|---|
| Drug Treatment | 64.9% | 60.1% |
| Prevention (Vaccine/Biological) | 0.9% | 5.1% |
| Infection Control/Behavioral | 5.3% | 3.7% |
| Combination Therapy | 1.8% | 1.6% |
| Diagnostic/Device | 1.8% | 2.5% |
| Other | 25.4% | 27.0% |

These results show an interesting result when looking through the lens of the 2015 WHO GAP. Their third pillar called for a reduction of incidence of infection, which would be "Infection Control/Behavioral", yet our results show this field decreased while fields like "Prevention (Vaccine/Biological)" increased. This shows that the majority of response continued to be biological response, rather than behavioral.

**Recommendation:** Policy frameworks should incentivize infection control behavioral trials more explicitly, as these represent low-cost, high-impact interventions that remain underfunded relative to drug development.

 
### Pillar 4 — Optimize Use
 
**Finding: Trial focus shifted from MRSA toward emerging critical threats (CRE, MDR-TB)**
 
| Resistance Type | Pre-WHO GAP | Post-WHO GAP |
|---|---|---|
| MRSA | 26 | 10 |
| MDR-TB | 4 | 12 |
| CRE | 1 | 17 |
| XDR-TB | 2 | 4 |
| VRE | 1 | 4 |
 
The most striking finding in this analysis is the **17-fold increase in CRE trials** (1 → 17) post-WHO GAP. Carbapenem-resistant Enterobacteriaceae represent one of the most urgent AMR threats, carbapenems are often the last-line treatment for gram-negative infections, and resistance leaves clinicians with few remaining options. The near-absence of CRE trials pre-2015 followed by a dramatic increase post-WHO GAP is the clearest evidence of policy-driven research reorientation in this dataset.
 
The decline in MRSA trials (26 → 10) is not cause for concern, it reflects a maturing pipeline where established treatments (vancomycin, linezolid, daptomycin) have reduced the urgency of new MRSA-specific development.
 
**Recommendation:** The CRE pipeline, while growing, remains small in absolute terms. Targeted funding mechanisms (similar to CARB-X or BARDA's AMR program) should continue to prioritize carbapenem-resistant gram-negative organisms where treatment options are most critically limited.


### Pillar 5 — Sustainable Investment
 
**Finding: Median enrollment grew 72% (100 → 172 participants)**

<img width="1836" height="828" alt="image" src="https://github.com/user-attachments/assets/3d471365-68ce-4cb3-acfe-87937cb72cf8" />


Larger trials require more funding, the 72% increase in median enrollment post-WHO GAP suggests greater resource commitment per trial, not just more trials. This is a meaningful indicator of deepening investment beyond surface-level registration activity.
 
**Finding: Late-stage trials increased from 50% to 59.5% of the pipeline**

 <img width="1476" height="877" alt="image" src="https://github.com/user-attachments/assets/92369fe6-9435-4241-9670-4a0bfda94b5c" />
 

 | Phase | Pre-WHO GAP | Post-WHO GAP |
|---|---|---|
| Phase 1 | 13.3% | 14.6% |
| Phase 1/2 | 3.3% | 4.5% |
| Phase 2 | 33.3% | 21.3% |
| Phase 2/3 | 3.3% | 12.4% |
| Phase 3 | 20.0% | 21.3% |
| Phase 4 | 26.7% | 25.8% |
| **Late stage (Phase 2/3+)** | **50.0%** | **59.5%** |

The post-WHO GAP cohort shows a higher proportion of late-stage trials (59.5%) than the pre-WHO GAP cohort (50.0%). This finding becomes significantly more compelling when accounting for time. Pre-WHO GAP trials have had a decade or more to mature through the pipeline, meaning their 50% late-stage rate reflects years of natural progression. Post-WHO GAP trials have had considerably less time to advance yet already exceed that benchmark at 59.5%. This suggests that post-2015 AMR trials entered the pipeline at a more advanced stage of development, reflecting greater upfront investment and scientific readiness, a sign that the WHO GAP may have produced not just more research activity but more mature, better-resourced research programs from the jump.

**Finding: Industry sponsorship declined slightly (38% → 35.6%) while government entered the space**
 
| Sponsor Type | Pre-WHO GAP | Post-WHO GAP |
|---|---|---|
| Academic/Research | 62.0% | 62.8% |
| Industry | 38.0% | 35.6% |
| Government | — | 1.7% |
 
This is the most policy-relevant and concerning finding in the analysis. Despite the WHO GAP's explicit goal of stimulating sustainable investment, industry's share of AMR trial sponsorship *declined* post-2015. Academic and research institutions continue to shoulder the majority of the trial burden (62%+), while government sponsorship — though newly present post-2015 — remains marginal at 1.7%.
 
**Recommendation:** The WHO GAP succeeded in raising awareness and stimulating academic research activity, but has not yet achieved its goal of sustainable private sector investment in AMR. There needs to be some market-entry reward for companies that are able to create solutions to this rising AMR problems. In the current economic landscape it is evident it is just not reasonable to pursue this type of research. 

### Completion Rates — A Note on Active Trials
 
| Status | Pre-WHO GAP | Post-WHO GAP |
|---|---|---|
| Completed | 79.0% | 52.1% |
| Active | 1.6% | 39.5% |
| Terminated | 11.3% | 6.3% |
| Withdrawn | 8.1% | 2.1% |
 
The lower completion rate post-WHO GAP (52.1% vs 79.0%) is expected rather than alarming — 39.5% of post-2015 trials are still actively running. As these trials complete over the next 3-5 years, the completion rate will likely converge toward pre-2015 levels. The decline in termination (11.3% → 6.3%) and withdrawal (8.1% → 2.1%) rates is a positive signal suggesting better trial design and execution in the post-WHO GAP era.
 
---

### Summary of Key Findings
 
| WHO GAP Pillar | Finding | Signal |
|---|---|---|
| Awareness & Knowledge | 236.6% increase in trial volume | ✅ Strong response |
| Awareness & Knowledge | Pathogen diversity expanded from 6 to 9 groups | ✅ Moderate response |
| Reduce Infection | Prevention trials grew from 0.9% to 5.1% | ⚠️ Partial response |
| Optimize Use | CRE trials grew 17x; focus shifted to emerging threats | ✅ Strong response |
| Sustainable Investment | Enrollment +72%, late-stage trials +9.5pp | ✅ Moderate response |
| Sustainable Investment | Industry share declined from 38% to 35.6% | ❌ Gap remains |
 
---
 
*Data sourced from AACT static download (ClinicalTrials.gov). To reproduce this analysis, restore the AACT PostgreSQL dump locally following the instructions in `sql/setup.md`, then run notebooks in sequence: `01_eda.ipynb` → `02_cleaning.ipynb` → `03_analysis.ipynb`.*

