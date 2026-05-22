# AMR Clinical Trial Landscape
### Evaluating the Research Response to the WHO Global Action Plan on Antimicrobial Resistance
---
## 1. Question 
**AMR Clinical Trial Landscape: Did the Research Pipeline Respond to the Global AMR Crisis?**
Analyzing 312 AMR-specific clinical trials from ClinicalTrials.gov to evaluate whether trial volume, phase distribution, enrollment, and sponsor landscape shifted following the 2015 WHO Global Action Plan on Antimicrobial Resistance. Built with PostgreSQL and Python.

**Tools:** PostgreSQL · Python · pandas · matplotlib · seaborn · Jupyter  
**Data Source:** [AACT (Aggregate Analysis of ClinicalTrials.gov)](https://aact.ctti-clinicaltrials.org/) — maintained by the Clinical Trials Transformation Initiative (CTTI)


## 2. Summary

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

Critically, the analysis also surfaces a policy-relevant gap: **indsutry sponsorship declined slightly** from 38% to 35.6% post-WHO GAP, while academic and government institutions absorbed the growing trial burden. This raises important questions about the sustainability of AMR research and whether or not there will be a more delayed response by industry to this problem. 

---

## 3. Business Problem
 
Antimicrobial resistance represents one of the most complex challenges in modern medicine. Unlike most therapeutic areas, AMR drug development is economically unattractive. If a new "wonderdrug" antibiotic is creating, it is immediately strictly rationed in fears of pathogens developing immunity. This inherently means much lower sales as well. 

The WHO GAP was designed in part to address this market failure by coordinating international policy, funding, and research prioritization.
 
**The core analytical question:** In the decade following the 2015 WHO Global Action Plan, did clinical trial activity reflect the five pillars of the framework?
 
This is examined across five dimensions:
 
- **Pillar 1 & 2 — Awareness & Knowledge:** Did trial volume and pathogen diversity increase?
- **Pillar 3 — Reduce Infection:** Did trial focus shift toward prevention and infection control?
- **Pillar 4 — Optimize Use:** Did trials targeting specific resistance mechanisms grow? Did combination therapy increase?
- **Pillar 5 — Sustainable Investment:** Did enrollment scale, late-stage trial rates, and industry engagement grow?
---

 
