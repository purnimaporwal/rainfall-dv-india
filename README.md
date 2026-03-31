# Rainfall, Agriculture & Domestic Violence Against Women in India 🌧️

**MSc Dissertation | University of Nottingham | 2024**

**Grade: 68 — High Merit**

**Examiner feedback (first marker):**
> "The dissertation tackles an important and well-defined question with impressive data collection and a deep understanding of the institutional context. The novelty of combining climate, agricultural, and social outcomes in a single framework is a strong aspect of the study."

**Conference:** Abstract accepted for poster session at the Population Association of America (PAA) Annual Meeting 2026. Unable to attend due to funding constraints and current IFAD internship commitments.

This is the repository for my MSc dissertation analysis. I was trying to answer a specific question: do rainfall shocks increase domestic violence against women in India by reducing agricultural income?

---

## The research question

The income stress channel made sense to me theoretically. Less rain means lower agricultural output, lower household income, more economic stress, and potentially more violence at home. I wanted to see if the data actually showed this.

---

## What I found

I built a state-level panel dataset covering 25 Indian states from 2001 to 2021, using data from IMD for rainfall, NCRB for crime, and RBI for agricultural and financial data.

The results were more interesting than I expected.

```
Rainfall deviation → lower agricultural output            ✓  (significant)
Rainfall deviation → more domestic violence (direct)      ✗  (minimal effect)
Social sector expenditure → MORE reported violence        ✓  (unexpected, robust)
```

The direct rainfall-to-violence channel was weak. Rainfall significantly affected agricultural output, but that effect did not translate directly into more reported domestic violence.

What was unexpected was the social sector expenditure finding. States that spend more on health and education reported more domestic violence, not less. That result held across all my specifications.

---

## My interpretation (developed after the dissertation)

This interpretation came after finishing the dissertation, through continued reading. It is a hypothesis, not a finding from the dissertation itself. I want to be clear about that.

I think what the data shows is not more violence occurring. More violence is being reported. When women have a clinic to go to, a school nearby, a government presence they can approach, they are more likely to report violence that was always happening but was previously invisible in the data.

I am calling this the institutional trust mechanism. I am still developing the theoretical framework for it and working on a more rigorous version of this paper that addresses the identification challenges more carefully.

---

## Data sources

| Variable | Source | Coverage |
|---|---|---|
| Domestic violence (reported incidents) | NCRB Crime in India reports | 2001–2021, 25 states |
| Annual rainfall deviation | IMD (India Meteorological Department) | State-level, annual |
| SW Monsoon rainfall deviation | IMD | State-level, annual |
| Agricultural output | RBI Handbook of Statistics on Indian Economy | State GDP from agriculture |
| Net irrigated area | RBI | State-level |
| Credit to agriculture | RBI | State-level |
| Social sector expenditure | RBI State Finances | Education + health spend |

The raw dataset is not uploaded here due to file size. The variable names and sources above are enough to reconstruct it from the original public sources.

---
## Methods

*The full analysis do-file is being cleaned and will be uploaded shortly. The core specifications below match the published paper.*

**Panel setup:**
```stata
encode STATE, generate(STATE_id)
xtset STATE_id YEAR
```

**Main specification — fixed effects with year dummies:**
```stata
xtreg DomesticViolenceIncidents AgriculturalOutput AnnualRainfalldeviation ///
    SWMonsoonRainfallDeviation NetIrrigatedArea ///
    CredittoAgriculturebySchedul SocialSectorExpenditure i.YEAR, fe
```

**Robustness checks I ran:**
- Hausman test (FE vs RE)
- Breusch-Pagan LM test (xttest0)
- Clustered standard errors (vce(cluster STATE_id))
- VIF multicollinearity diagnostics
- Correlation matrix
- Residual diagnostics (scatter, histogram, Q-Q plot)
- Coefplots for coefficient visualisation

---

## Repository contents

```
rainfall-dv-india/
│
└── README.md                # This file
```

**Code:** The Stata do-file is being cleaned and annotated before I upload it. A working version with the full exploratory analysis exists. It will be added once it has a clear structure, a global path variable, and proper comments explaining each step. That is the standard I want for anything I share publicly.

**Data:** Not uploaded due to file size. All sources are publicly available from IMD, NCRB, and RBI. The data sources table above has everything needed to reconstruct the dataset.

---

## Status and what I am working on

The dissertation was submitted and graded in 2024.

Since then, I have kept reading. The IPV literature, institutional economics, measurement theory, and research on how hidden outcomes become visible through institutional presence. I am trying to develop the institutional trust mechanism into a proper theoretical framework with stronger identification. That work is ongoing.

This repository will be updated as the work develops. The cleaned do-file is coming.

If you work on related questions, domestic violence measurement, institutional trust, climate and gender outcomes in South Asia, I would genuinely love to talk.

---

## Citation

Porwal, P. (2024). "Rainfall Variations, Agriculture and Domestic Violence Against Women in India." MSc Dissertation, University of Nottingham.

Also published: [open-access journal version](https://ijmrrs.com/wp-content/uploads/2025/01/DevelopmentEconomics_Research-1.pdf)

---

Part of my research portfolio: [github.com/purnimaporwal](https://github.com/purnimaporwal)

*Author: Purnima Porwal | porwal.purnima18@gmail.com*
