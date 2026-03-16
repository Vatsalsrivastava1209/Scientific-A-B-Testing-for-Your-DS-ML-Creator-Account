# Tweet Experiment – A/B Testing on X (Twitter)

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

Interpretation:

* **p < 0.05** → statistically significant difference
* **p ≥ 0.05** → no significant difference

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

**Vatsal**

LinkedIn
https://www.linkedin.com/in/vatsal-srivastava-440417260/
