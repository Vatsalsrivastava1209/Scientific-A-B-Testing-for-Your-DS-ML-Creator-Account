# Tweet Experiment Lab – A/B Testing on X (Twitter)

## Overview

This project is a real-world experimentation study where I run a **randomized A/B test on my own X (Twitter) account** to measure which tweet structure generates higher engagement.

Instead of guessing what works on social media, this project applies **data science experimentation principles** such as:

* Power analysis
* Randomized controlled experiments
* Hypothesis testing
* Statistical significance testing
* Data visualization

The goal is to determine whether **question-based tweet hooks outperform statement-based hooks** in driving engagement.

This project demonstrates how **A/B testing frameworks used in tech companies can be applied to real-world social media growth problems.**

---

## Experiment Hypothesis

**Hypothesis**

> If tweets start with a **question hook**, then engagement will increase compared to a **statement hook**, because questions trigger curiosity and encourage replies.

---

## Experiment Design

### Variants

**Variant A – Statement Hook**

```
Most data analysts build dashboards.

Very few build dashboards that actually drive revenue.
```

**Variant B – Question Hook**

```
Why do most dashboards fail to drive revenue?
```

Only the **hook format changes**.
The rest of the tweet content remains similar to control the experiment.

---

## Primary Metric

Engagement per tweet:

```
engagements = likes + replies + reposts + bookmarks
```

This metric captures how much interaction each tweet generates.

---

## Power Analysis

Before running the experiment, a statistical power analysis was performed to determine the required sample size.

Assumptions:

* Baseline engagement: ~2 engagements per tweet
* Expected improvement: 100%
* Significance level (α): 0.05
* Statistical power: 0.80

Python code used:

```python
from statsmodels.stats.power import TTestIndPower

baseline_mean = 2
expected_lift = 1.0
std_dev = 2

new_mean = baseline_mean * (1 + expected_lift)

effect_size = (new_mean - baseline_mean) / std_dev

analysis = TTestIndPower()

sample_size = analysis.solve_power(
    effect_size=effect_size,
    power=0.8,
    alpha=0.05
)

print(round(sample_size))
```

Result:

```
17 tweets per variant
```

Total experiment size:

```
34 tweets
```

---

## Randomization

To prevent bias, tweet variants were randomly assigned using Python.

Example code:

```python
import random
import pandas as pd

n_per_variant = 17

variants = ["A"] * n_per_variant + ["B"] * n_per_variant
random.shuffle(variants)

df = pd.DataFrame({
    "tweet_number": range(1, len(variants) + 1),
    "variant": variants
})
```

This ensures the experiment behaves like a **randomized controlled trial (RCT)**.

---

## Data Collection

For each tweet the following metrics are recorded:

* Likes
* Replies
* Reposts
* Bookmarks

Example dataset structure:

```
tweet_number,variant,likes,replies,reposts,bookmarks
1,A,3,1,0,0
2,B,5,2,1,0
```

Engagement is calculated as:

```python
df["engagements"] = (
    df["likes"] +
    df["replies"] +
    df["reposts"] +
    df["bookmarks"]
)
```

---

## Statistical Analysis

A **two-sample t-test** is used to compare the mean engagement between the two variants.

```python
from scipy.stats import ttest_ind

A = df[df.variant=="A"]["engagements"]
B = df[df.variant=="B"]["engagements"]

t_stat, p_value = ttest_ind(A, B)
```

Interpretation:

* **p < 0.05** → statistically significant difference
* **p ≥ 0.05** → no significant difference

---

## Visualization

The results are visualized to compare engagement distributions.

Example:

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.boxplot(data=df, x="variant", y="engagements")
plt.title("Tweet Engagement A/B Test")
plt.show()
```

---

## Project Structure

```
tweet-ab-testing-lab/

data/
    experiment_results.csv

notebooks/
    01_power_analysis.ipynb
    02_randomization.ipynb
    03_metrics.ipynb
    04_analysis.ipynb

README.md
```

---

## Skills Demonstrated

This project demonstrates practical data science skills:

* Experimental design
* A/B testing methodology
* Power analysis
* Statistical hypothesis testing
* Data analysis using Python
* Reproducible experimentation workflows

These are the same experimentation techniques used in product analytics teams at companies like Netflix, Airbnb, and Meta.

---

## Future Improvements

Possible extensions of this project:

* Bayesian A/B testing
* Multi-armed bandit algorithms
* Thread vs single tweet experiments
* Emoji usage experiments
* Posting time optimization

---

## Author

**Vatsal Srivastava**

Data analyst focused on experimentation, analytics, and product insights.

LinkedIn
https://www.linkedin.com/in/vatsal-srivastava-440417260/
