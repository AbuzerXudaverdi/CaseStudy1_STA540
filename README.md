# CTN-0083 Replication Study

**Author:** Abuzar Khudaverdiyeva
**Date:** January 28th
**Course:** STA540L

---

## 1. Study Overview

### Background and Motivation
There are a lot of different types of online platforms to promote home HIV self-testing.
But there's not much data/study about which type of platform (social media, information search sites, or dating apps) 
could be the most efficient to promote it. This study evaluated 6 online platforms to compare the efficiency of them for 
promoting HIV self-testing among MSM (men who have sex with men).

### Primary Objective
The primary objective was to compare the effectiveness of promoting HIV self-test kits among three types of online platforms: 
Social media sites (Facebook, Instagram, Twitter), search engines (Google, Bing, Yahoo), versus dating apps (Grindr, Jack'd, Hornet). Due to 
low enrollment, 3rd wave of promotion (included Twitter, Yahoo, and Hornet) was not included in the study.

### Secondary Objectives
The secondary objectives were to examine baseline characteristics and behavior of participants. The study compared participants 
who ordered a kit versus those who did not based on:

- Tobacco, alcohol, prescription medications, and other substance use
- Stage of Health Behavior Change
- Attitudes toward human immunodeficiency virus (HIV) testing
- Attitudes toward human immunodeficiency virus (HIV) treatment 
- Human immunodeficiency virus (HIV)-related stigma among study participants
- Medical mistrust

---

## 2. Replicated Table 1

### Methods

I excluded 17 people who were either enrolled in wave 3 (researchers stated they 
did not include people from wave 3) or people who were enrolled in early wave 1 
(when Grindr was inactive). Also data dictionary mentions a variable called PO_FLAG (
Primary Outcome Analysis Flag -Include/Do not include), which was very useful to
filter all 254 participants enrolled. All characteristics listed in  Study Table 1
were included in this replication Table 1.


### Results

**Table 1: Baseline Characteristics Comparison**

| Characteristic |   Replication  | Manuscript | 
|----------------|----------------|------------|
| **Age, median (IQR)** | 25 (21-27) | 25 (23-27) | 
| **Ethnicity** | | |
| Hispanic/Latinx, n (%) | 66 (26) | 66 (26) |
| **Race, n (%)** | | | |
| American Indian/Alaskan Native | 1 (0.4) | 1 (0.4) | 
| Black/African American | 96 (78.4)| 196 (78.4) | 
| White | 28 (11.2) | 28 (11.2) | 
| Other | 14 (5.6) | 14 (5.6) | 
| Multiracial | 11 (4.3) | 11 (4.4) | 
| **History of PrEP uptake, n (%)** | | | 
| Never taken PrEP | 232 (91.3) | 232 (91.3) | 
| In the past 6 months | 22 (8.7) | 22 (8.9) | 
| **Male sex partners (past 90 days), median (IQR)** | 4 (3-6) | 4 (3-6) | 
| **Condom use, n (%)** | | | 
| Never | 36 (14.2) | 36 (14.2) | 
| Sometimes |  108 (42.5) | 108 (42.5) | 
| About half the time | 37 (14.6) | 37 (14.5) | 
| Most of the time | 68 (26.8) | 68 (26.8) | 
| Always | 5 (2.0)  | 5 (2.0) | 
| **Condomless receptive anal sex (past 90 days), n (%)** | 210 (82.7) | 210 (82.7) |
| **Ever tested for HIV, n (%)** |  191 (75.2)| 191 (75.2) |
| **If tested for HIV, median months since (IQR)** | 11 (6-21) | 11 (6-21) | 
| **If not tested for HIV, n (%)** | 63 (24.8) | 63 (24.8) | 
| **Main reasons cited by 63 participants for not getting tested, n (%)** | | |
| Unlikely to be exposed to HIV | 8 (12.7) | 8 (12.7) |
| Afraid of testing HIV-positive | 26 (41.3) | 26 (41.3) |
| Did not want to think about HIV/HIV-positive | 8 (12.7) | 8 (12.7) |
| Worried about names being reported if positive | 3 (4.8) | 3 (4.8) |
| Dislike for needles | 5 (7.9) | 5 (8) |
| Unable to trust that results will be confidential | 3 (4.8) | 3 (4.8) |
| Unaware of where to get tested | 7 (11.1) | 7 (11.1) |
| Other reasons | 3 (4.8) | 3 (4.8) |
**Summary:** Most of the characteristics seem to match except median age.

---

## 3. Replicated Results

### Primary Analysis: Poisson Regression

**Methods:**

I used a Poisson regression model as described in the manuscript. The model compared 
kit ordering rates across the six promotional platforms. The outcome variable was 
the number of test kits ordered from each web site. The predictor variable was 
the advertising site (Facebook, Grindr,  Google, Instagram, Jack'd, and Bing). 

Because those sites had different advertising durations (Wave 1 sites ran for 70 
days, but Wave 2 sites ran for 38 days), I included an offset term of log(advertising 
days) to account for the different exposure times. This allowed me to calculate 
and compare kit ordering rates (kits per day).

The model was:
```
glm(n_orders ~ site, offset = log(ad_days), family = poisson(link = "log"))
```

Then I used the emmeans package to extract site-specific order rates.

**Site-Specific Ordering Rates:**

| Wave.      | Site     | Rate (kits/day) |
|------------|----------|-----------------|
| **Wave 1** | Facebook | 0.186 |
| **Wave 1** | Grindr   | 0.129 |
| **Wave 1** | Google   | 0.243 |
| **Wave 2** | Instagram | 0.342 |
| **Wave 2** | Jack'd   | 3.289 |
| **Wave 2** | Bing     | 0.000 |

**Pairwise Comparisons:**

I conducted pairwise comparisons between sites within each wave using the emmeans 
package. Multiple testing correction was applied using the Benjamini-Hochberg 
method to control the false discovery rate.

**Wave 1 comparisons (Facebook vs. Grindr vs. Google):**
- Couldn't find any significant differences among any Wave 1 sites (all adjusted 
  p-values > 0.59)
- According to manuscript, they also had a similar result

**Wave 2 comparisons:**
- Jack'd vs. Instagram: Jack'd had a significantly higher ordering rate 
  (p < 0.001, adjusted)
- This matches the manuscript finding (p < 0.001)
- Couldn't find any other significant difference among Wave 2 sites, this could happen
because there were zero enrollments from Bing


### Secondary Analyses

**Table a:  Tobacco, alcohol, prescription medications, and other substance use**
- 4 of 6 substance categories successfully replicated (Alcohol p=0.35, 
Cannabis p=0.096, Stimulants p=0.299, Opioid p=1.0). Sedative and Prescribed 
stimulant p-values differ. There are some issues in the dataset. Public 
dataset shows n=61 missing values; while the manuscript indicates n=6 missing 
for column Q13_17 and Q13_20. I think this might be causing this discrepancy.

**Table b: Stage of Health Behavior Change**
Results:
- p-value: 0.252
- Manuscript p-value: 0.251

**Table c: Attitudes toward human immunodeficiency virus (HIV) testing**

| Statement                                       | Rep. p-value | Manuscript p-value |
|-------------------------------------------------|------------|-------------------|
| Getting tested for HIV helps people feel better | 0.160 | 0.160 |
| Getting tested for HIV helps people from getting HIV | 0.717 | 0.717 | 
| People in my life would leave if I had HIV | 0.035 | 0.035 | 
| People who tested positive for HIV should hide it from others | 0.825 | 0.825 | 
| I would rather not know if I have HIV | 0.463 | 0.463 |

**Table d: Attitudes toward human immunodeficiency virus (HIV) treatment**

| Statement              | Rep. p-value | Manuscript p-value | 
|------------------------|------------|-------------------|
| Less threatened by HIV+ | 0.421 | 0.421 |
| Less worried about HIV infection | 0.400 | 0.399 |
| HIV/AIDS less of a problem | 0.413 | 0.413 |
| HIV/AIDS less serious threat | 0.225 | 0.225 |
| Less concerned about becoming HIV+ | 0.274 | 0.274 |
| Condom use less necessary | 0.971 | 0.971 |
| HIV+ needs to care less about condoms | 0.064 | 0.064 |
| Need for condoms is less | 0.767 | 0.767 |
| HIV+ can be cured | 0.199 | 0.199 |
| Treatments can eradicate virus | 0.029 | 0.029 |



**Table e: e. Human immunodeficiency virus (HIV)-related stigma among study participants**

| Statement                                    | Rep. p-value | Manuscript p-value |
|----------------------------------------------|--------------|-------------------|
| I feel afraid of people living with HIV/AIDS | 0.613 | 0.613 |
| I could not be friends with someone who has HIV/AIDS | 0.032 | 0.033 | 
| People who get HIV/AIDS through sex or drug use got what they deserve | 0.332 | 0.332 |
| I feel anger toward people with HIV/AIDS | 0.213 | 0.213 | 



**Table f: Medical Mistrust (Wilcoxon rank tests)**

| Statement                                                            | Rep. p-value | Manuscript p-value |
|----------------------------------------------------------------------|---------------|-------------------|
| You'd better be cautious when dealing with health care organizations | 0.503 | 0.503 |
| Patients have sometimes been deceived or misled | 0.413 | 0.413 |
| When health care organizations make mistakes they usually cover it up | 0.222 | 0.222 |
| Health care organizations have sometimes done harmful experiments | 0.413 | 0.413 |
| Health care organizations don't always keep your information private | 0.371 | 0.371 |
| Sometimes I wonder if health care organizations really know what they're doing | 0.965 | 0.965 |
| Mistakes are common in health care organizations | 0.638 | 0.638 |


---

## 4. Reflections

### What Went Well
Replicating Table 1 and secondary Analyses (Table a-f) was mainly successful.
Most of the results matched manuscript very closely.


### Challenges 

**Challenge 1: Median Age**
Replicated median age was 25 (21-27), but manuscript indicated median age was 25(23-27).
Couldn't identify what caused the discrepancy between them.

**Challenge 2: Bing Advertising Site**
Bing data was not included in public dataset as there were no enrollments. So 
I had to manually enter values (0 order, 0 enrollment) for Bing to get complete 
order rate listing. Even though fitting regression model didnt cause issues, 
pairwise comparisons became challenging, so I couldn't replicate any pairwise result
involving Bing.


**Challenge 3: Missing Data Coding**
Columns 'Q13_17' (sedative use) and 'Q13_20' (prescribed stimulant use) had 61 
values coded as 9999 in the public dataset. These were treated as missing values 
in the replication, but the manuscript showed only 6 missing values for these variables. 
This, in turn, resulted in different p-values in replication. Rep. p-value was 0.21
for sedative use while manuscript reported 0.722. And Rep. p-value was 0.222 for
prescribed use, but manuscript showed 0.727.


---

## 5. References

**Primary Manuscript:**

Stafylis, C., Vavala, G., Wang, Q., McLeman, B., Lemley, S. M., Young, S. D., 
Xie, H., Matthews, A. G., Oden, N., Revoredo, L., Shmueli-Blumberg, D., 
Hichborn, E. G., McKelle, E., Moran, L. M., Jacobs, P., Marsch, L. A., & 
Klausner, J. D. (2022). Relative effectiveness of social media, dating apps, 
and information search sites in promoting HIV self-testing: Observational 
cohort study. *JMIR Formative Research, 6*(9), e35648. 
https://doi.org/10.2196/35648

**Study Data:**

National Institute on Drug Abuse. (n.d.). *CTN-0083: Social media HIV prevention 
study*. Retrieved from https://datashare.nida.nih.gov/study/nida-ctn-0083

**Statistical Methods and Software:**


Lenth, R. V. (2024). *emmeans: Estimated Marginal Means, aka Least-Squares Means*. 
R package. https://CRAN.R-project.org/package=emmeans




