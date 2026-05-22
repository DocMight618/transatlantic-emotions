# Transatlantic Emotions: An Emotional Perspective on Alliance Burden Sharing

**Author:** Haoyan "Ken" Wang  
**Institution:** The University of Chicago — Master of Arts in Computational Social Science  
**Date:** May 2026  
**Faculty Advisor:** Dr. Paul Poast, Department of Political Science  
**Preceptor:** Dr. David A. Peterson, Master of Arts in Computational Social Science

---

## Abstract

This paper examines how emotions expressed in U.S. presidential speeches influence NATO allies' defense spending behavior in the post-Cold War period. Using a custom Python scraper, the author collected 8,137 NATO-relevant speeches from the American Presidency Project and applied the DistilBERT large language model to quantify six emotions — anger, fear, sadness, joy, disgust, and surprise — in each speech. These emotion scores were incorporated into an original country-year panel dataset and tested using multiple regression models. Results show that **anger, fear, and sadness** are the most statistically significant emotions. Notably, presidential anger is positively associated with allied defense spending (interpreted as appeasement), while fear and sadness are negatively associated with it.

---

## Repository Contents

| File/Folder | Description |
|---|---|
| `Transatlantic Emotions Dataset` | Cleaned Transatlantic Emotions Dataset (TED) |
| `requirements` | Required libraries used in the Jupyter notebbok and R Markdown file |
| `Topic EI Analysis` | Jupyter notebook visualizations |
| `Transatlantic Emotions` | R Markdown file for regression models |

**Contact:** Haoyan Wang — hkwang925@gmail.com

---

## Section Summaries

### 1. Introduction

The paper is motivated by the ongoing debate over NATO burden sharing, particularly the U.S. push for allies to meet defense spending targets (2% of GDP at the Wales Summit in 2014, and 5% at the Hague Summit in 2025). The author argues that while the U.S. primarily uses rhetorical tools — embedded in presidential speeches — to pressure allies, the emotional dimension of this rhetoric has been overlooked. The paper asks: *how do emotions in U.S. presidential speeches affect NATO allies' defense spending behavior?* The author previews four contributions: a new dataset, six emotion-specific hypotheses, a theoretical framework for under-studied emotions, and a novel NLP methodology for quantifying emotional intensity.

---

### 2. Literature Review

This section reviews three bodies of scholarship:

- **Leading States in Alliances:** Draws on realist, institutionalist, and constructivist theories to explain why states cooperate and how leading states (like the U.S. in NATO) shape alliance dynamics. Identifies a gap: existing theories operate at the international or national level and ignore the individual leader.

- **Emotions in International Politics:** Surveys a growing but still limited literature on emotion in IR. Identifies four functions of strategic emotion — communication, sense-making, mobilization, and discipline — and argues that emotional expression is rational and strategic, not irrational. Highlights three gaps: (1) no reliable way to measure emotional effectiveness, (2) conflation of leaders' emotions with collective state emotions, and (3) no theories about specific individual emotions.

- **NATO Burden Sharing:** Reviews the history of uneven defense contributions within NATO. Notes that the burden-sharing structure shifted after 9/11, and that diverging U.S.–European interests, EU fiscal constraints, and intra-alliance competition all complicate collective defense commitments.

---

### 3. Hypotheses

The author develops one hypothesis for each of the six emotions:

| Hypothesis | Emotion | Predicted Effect on NATO Allies' Defense Spending |
|---|---|---|
| H1 | **Anger** | Increase (appeasement of an angry hegemon) |
| H2 | **Fear** | Decrease (lack of shared fears between U.S. and allies) |
| H3 | **Joy** | No change or slight increase (positive reinforcement) |
| H4 | **Sadness** | Decrease (signals pessimism/lack of confidence in alliance) |
| H5 | **Disgust** | Decrease (fosters enmity; signals normative divergence) |
| H6 | **Surprise** | Decrease (signals uncertainty; allies distance themselves from costly actions) |

---

### 4. The Transatlantic Emotions Dataset (TED)

The author constructs an original country-year panel dataset covering **29 NATO allies from 1993 to 2023** (excluding Sweden, which joined in 2024, and Iceland, which has no standing army).

**Dependent Variable:**
- `RDef` — annual national defense spending as a percentage of total government spending (source: SIPRI)

**Independent Variables:**
- Annual average emotional intensity scores for each of the six emotions, extracted from presidential speeches using DistilBERT

**Control Variables:**
- `Sentiment` — general positive/negative tone of speeches, scored –1 to 1 using BART-Large-MNLI
- `Dem` — V-Dem Liberal Democracy Index (0 to 1)
- `IntrastCon` — number of intrastate conflicts per year (proxy for global security environment)

**Dummy Variables:** `NATO` and `EU` membership by year (accounting for enlargement over time)

**Alternative Variables:** EU Fiscal Rule Index (FRI) and log-transformed distance from each ally's capital to Moscow (Proximity)

---

### 5. Methodology

The core analytical approach is **unsupervised sentiment analysis** using transformer-based large language models, which avoids human labeling bias. Speeches were scraped from the American Presidency Project, filtered by the keyword "NATO," and run through DistilBERT to extract emotional intensity scores.

Four regression models are estimated, each run four times (with/without control variables and country fixed effects):

1. **Raw Analysis** — full dataset, all allies
2. **European Model** — subset of EU member states (24 of 27 EU members are also NATO members)
3. **Democrat Model** — presidential speeches from Democratic administrations only
4. **Republican Model** — presidential speeches from Republican administrations only

All variables are **lagged by one year** to account for the federal budget cycle. Two alternative models test competing explanations: the **FRI Model** (EU fiscal rules) and the **Proximity Model** (distance to Moscow).

---

### 6. Results and Discussion

**Main Findings:**

- **Anger (H1 supported):** Positively and significantly correlated with allied defense spending, but only when country fixed effects are included. Allies appear to appease an angry U.S. president by spending more — consistent with historical patterns of appeasement as a survival strategy.

- **Fear (H2 supported):** Negatively and significantly correlated with defense spending across all main models. The U.S. and its allies do not share the same fears (e.g., immigration vs. democratic backsliding), so presidential fear does not motivate allied spending.

- **Sadness (H4 supported):** Negatively and significantly correlated with defense spending. Presidential sadness signals pessimism about the alliance and does not translate into allied action.

- **Joy, Disgust, Surprise (H3, H5, H6 mixed/not supported):** These emotions are inconsistent across models. Joy is negatively correlated with spending in the Democrat Model, possibly because allies free-ride when a friendly president expresses satisfaction. Disgust is significant only in the Democrat Model.

**Partisan Differences:** NATO allies are more responsive to Democratic presidents than Republican ones. The Democrat Model yields more significant results across emotions; the Republican Model shows almost no significant effects, possibly reflecting NATO allies' perception of Republicans as less committed to the alliance.

**Control Variables:** Negative sentiment and lower democracy levels are both associated with higher defense spending. Intrastate conflict has a statistically significant but very small effect.

**Alternative Explanations:**

- **FRI Model:** EU fiscal rules lose statistical significance when emotions are included in the model, suggesting that emotional signals from the U.S. president matter more to European allies than fiscal constraints.
- **Proximity Model:** Counterintuitively, proximity to Russia is negatively correlated with defense spending in the post-Cold War period, contradicting prior research. When emotions are included, proximity loses much of its explanatory power.

---

### 7. Conclusion

The paper concludes that non-material factors — specifically presidential emotions — have measurable effects on allies' defense spending behavior. Anger, fear, and sadness are the most consistent predictors across models, supporting three of the six hypotheses. The research makes three main contributions: (1) a new NLP-based methodology for quantifying emotions in diplomatic speech at scale; (2) a theoretical bridge between leader-level emotional expression and collective security commitments; and (3) an original panel dataset linking emotional intensity to international security outcomes.

**Limitations** include unequal sample sizes between Democrat and Republican models (three Democratic vs. two Republican presidents in the post-Cold War period), the exclusion of the Cold War period and Sweden, and the limited ability of current LLMs to reliably detect positive emotions like joy in security-related texts.

**Future research** directions include extending the time horizon back to 1949, testing alternative LLM architectures better suited to positive emotion detection, and incorporating Sweden now that it has joined NATO.

---

## Data & Code Availability

Cleaned data, Python scraping scripts, Jupyter notebooks, and R Markdown analysis files are available in this GitHub repository. For supplementary materials, contact the author at **hkwang925@gmail.com**.

---

## License
 
This work is licensed under a [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
 
You are free to share and adapt this material for any purpose, including commercially, as long as you give appropriate credit to the author:
 
> Wang, Haoyan "Ken". *Transatlantic Emotions: An Emotional Perspective on Alliance Burden Sharing.* Master of Arts thesis, The University of Chicago, May 2026.
 
[![CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](https://creativecommons.org/licenses/by/4.0/)
 
---

## Generative AI Statement

ChatGPT was used to assist with debugging the Python scripts and sentiment analysis pipeline. All other components of the paper are original work of the author.
