# M5 Choice Assignment: Regression

## Overview

This is a choice programming assignment for SEIS-631: Data Preparation and Analysis. This assignment begins with you requesting data for a specific make/model and locations using the car-listings request form linked on Canvas.

You will apply the regression model from class to a vehicle of your choosing and use it to find listings that are priced unusually well — or unusually poorly — relative to comparable vehicles.

### What does successful work look like?

A strong submission applies the full regression workflow end-to-end: cleaning and filtering the data thoughtfully, fitting the OLS model correctly, and — most importantly — interpreting the results in plain English. The written responses to the `Q:` questions are the heart of this assignment. Code that runs without errors but has blank or superficial answers will not earn full marks. Aim for responses that connect the numbers to real-world meaning.

## Learning Objectives

By the end of this assignment you should be able to:

- Load, clean, and filter a real-world dataset to prepare it for regression
- Engineer features (vehicle age, log-transformed odometer, location indicator) and explain why each transformation is useful
- Fit an OLS regression model using `statsmodels` and read the summary output
- Interpret regression coefficients — including a log-transformed predictor — in terms of dollars and miles
- Use model residuals to identify listings that are priced unusually high or low relative to model predictions
- Reflect critically on what a model captures and what it leaves out

## Data

You will request data using the car-listings request form linked on Canvas. This dataset will arrive in a zip file and be tab-delimited. It will match the format of the car listings dataset we've been using in class.

The dataset contains car listings scraped from Craigslist. See the Assignment 1 README for full column documentation. The columns most relevant to this assignment are:

| Column       | Description                                              |
|--------------|----------------------------------------------------------|
| `make`       | Vehicle manufacturer (e.g., ford, toyota)                |
| `model`      | Vehicle model (e.g., f150, camry)                        |
| `location`   | City where the listing was posted                        |
| `title`      | Title status (e.g., clean, salvage, rebuilt, lien)       |
| `price`      | Asking price in U.S. dollars                             |
| `year`       | Vehicle model year                                       |
| `odometer`   | Reported odometer reading (miles)                        |
| `time_posted`| Date and time the listing was posted                     |

**Never commit data files to Git.** The `.gitignore` is set up to exclude them, but don't fight it — no data in the repo. Here is a [Reddit thread](https://www.reddit.com/r/mlops/comments/13s716f/give_me_one_good_reason_why_i_shouldnt_keep_my/) that describes some of the reasons not to commit your data.

## Tasks

Work through the notebook (`Regression.ipynb`) from top to bottom. Questions to answer appear in cells marked `Q:` — answer them in Markdown. The notebook is divided into five parts:

### Part 1: Data Preparation

Run the provided cleaning pipeline, then handle missing and extreme values in the key columns. Filter to clean- or lien-title listings and engineer three features: `age` (vehicle age at time of listing), `log_odometer` (natural log of odometer), and `in_focal_location` (indicator for your chosen city). Answer the written questions about your filtering choices.

### Part 2: Exploring Your Data

Before fitting anything, look at the variables individually and together. Create a histogram of price and compute summary statistics. Create scatterplots of price vs. raw odometer, price vs. log-odometer, and price vs. age. Answer the written questions about what you observe.

### Part 3: Fitting the Model

Fit the OLS model from the in-class exercise using `smf.ols()`. Examine the summary output and interpret the key coefficients — especially `car_age` and `log_odometer` — in plain English using realistic dollar and mileage values. Discuss R-squared and what it tells you about model fit.

### Part 4: Finding Good and Bad Deals

Compute predicted prices and residuals for every listing. Plot the residual distribution. Flag listings more than 2 standard deviations below the prediction as potential good deals, and listings more than 2 standard deviations above as potentially overpriced. Examine specific listings and consider what the model might be missing.

## Reflection

End your notebook with a short written reflection (a few paragraphs, Markdown). Address:

- What was confusing, and how did you resolve it?
- Where did AI help you most? Where did it mislead you or produce something you had to fix?
- What do you understand now that you didn't before starting?
- How long did it take? Any unresolved questions?

## Deliverables & Submission

When you have completed your work, **follow these steps carefully before submitting**. They're the same on every assignment.

### 1. Restart & Clear Outputs

In the notebook menu, select **Kernel → Restart & Clear Output**. This removes all generated output and resets the kernel.

### 2. Run everything top to bottom

Select **Run → Run All Cells**. Scroll through the notebook, looking for errors, checking that outputs appear as expected, and **reading your Markdown cells**. These cells should be polished and complete, just as you'd review an essay before submitting it. This step proves your notebook doesn't depend on out-of-order execution and that I'll see the same results you do.

### 3. Commit and push to GitHub

You can commit and push using the GUI tools in VS Code or at the command line. 

```bash
git add "Regression.ipynb"
git commit -m "Ready for review"
git push
```

We'll typically use the VS Code Source Control GUI — instructions are in Module 0 on Canvas.

**Final checklist:**

- [ ] Kernel restarted and all outputs cleared
- [ ] All cells run successfully from top to bottom
- [ ] All `Q:` cells answered in Markdown
- [ ] Reflection written
- [ ] Changes committed and pushed to GitHub

## Working with AI

AI coding tools are allowed and expected in this course, from day one. You are not graded on hand-writing pandas; you are graded on asking the right statistical questions, verifying that the code does what you think it does, and interpreting results honestly.

Two rules of the road:

1. **You own every claim in your notebook.** "The AI wrote it" is not a defense of a wrong number, a mislabeled axis, or an overstated conclusion.
2. **Point your AI at `AGENTS.md`** in this repository. Agentic tools (Copilot agent mode, Cursor, Claude Code) will read it automatically; if you're using a chat tool, paste it in at the start. It tells your AI how to work with you so you actually learn something — small steps, checkpoints, no one-shot solutions.

The reflection asks where AI helped and where it misled you. Honest answers there are part of the work.

## Evaluation Criteria

This rubric describes levels of understanding and skill demonstration. Use it for self-assessment and to understand feedback. Your work is evaluated holistically — this shows what I'm looking for at each facet.

### Code Functionality

**Exemplary**: The notebook executes flawlessly top to bottom. All required tasks are completed correctly, and the notebook shows evidence that you *verified* the code does what you claim — sanity checks, spot checks against raw data, or commentary that demonstrates you know what each step accomplished.

**Proficient**: Executes with only minor issues that don't prevent completion of major tasks. Most tasks correct; errors are minor and don't indicate fundamental misunderstanding.

**Developing**: Some execution errors or incomplete tasks. Core functionality present but unverified — code appears pasted-and-hoped rather than checked.

**Beginning**: Does not run or has major errors. Multiple required tasks missing or fundamentally incorrect.

### Analysis & Interpretation

**Exemplary**: Every analytical question is answered correctly with a clear, plain-English explanation supported by the data. Claims are disciplined — they say what the data support, no more. Uncertainty is acknowledged where it exists. Visualizations directly support conclusions.

**Proficient**: Most questions answered correctly; minor calculation or interpretation errors, but claims stay tethered to evidence. Visualizations present but less clearly tied to the analysis.

**Developing**: Some answers incorrect or incomplete; some claims overreach what the data support. Visualizations rudimentary or absent.

**Beginning**: Many questions unanswered or incorrect. Conclusions disconnected from output. Limited evidence of analytical thinking.

### Finished Product

**Exemplary**: The notebook reads like a document, not a scratchpad. Markdown cells organize the workflow and carry commentary; variable names are meaningful; formatting is clean; a reader can follow the analysis without you in the room.

**Proficient**: Generally clean and readable; minor inconsistencies that don't impede understanding.

**Developing**: Works, but readability suffers — unclear names, weak organization, sparse commentary.

**Beginning**: Difficult to read or follow. Minimal attention to presentation.

### Reflection

**Exemplary**: Specific and honest. Names actual points of confusion and how they were resolved; identifies concretely where AI helped and where it misled; articulates something learned. Reads like it could only have been written by someone who did *this* assignment.

**Proficient**: Addresses the prompts with some specificity; engagement is evident but some answers stay general.

**Developing**: Generic — could have been written before starting the assignment. Little evidence of engagement with the actual experience.

**Beginning**: Missing or perfunctory.
