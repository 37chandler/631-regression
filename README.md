# Assignment: Regression

## Overview

This is a choice programming assignment for SEIS-631: Data Preparation and Analysis.
This assignment begins with you requesting data for a specific make/model and locations using this [Google Form](https://docs.google.com/forms/d/e/1FAIpQLSdQQMShcp2OaFkdOclqkJN5hmWjWsowEte62WrglmW1S61Vkw/viewform?usp=header).

You will apply the regression model from class to a vehicle of your choosing and use it to find listings that are priced unusually well — or unusually poorly — relative to comparable vehicles.




### What does successful work look like?

A strong submission applies the full regression workflow end-to-end: cleaning and filtering the data thoughtfully, fitting the OLS model correctly, and — most importantly — interpreting the results in plain English. The written responses to the `Q:` questions are the heart of this assignment. Code that runs without errors but has blank or superficial answers will not earn full marks. Aim for responses that connect the numbers to real-world meaning.

---

## Learning Objectives

By the end of this assignment you should be able to:

- Load, clean, and filter a real-world dataset to prepare it for regression
- Engineer features (vehicle age, log-transformed odometer, location indicator) and explain why each transformation is useful
- Fit an OLS regression model using `statsmodels` and read the summary output
- Interpret regression coefficients — including a log-transformed predictor — in terms of dollars and miles
- Use model residuals to identify listings that are priced unusually high or low relative to model predictions
- Reflect critically on what a model captures and what it leaves out

---

## Data

You will request data using the link above. This dataset will arrive in a zip file and be tab-delimited. It will match the format of the car listings dataset we've been using in class. **Do not commit the data file to Git.**

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

---

## Instructions

Work through the notebook (`Regression.ipynb`) from top to bottom. The notebook is divided into five parts:

### Part 1: Data Preparation
Run the provided cleaning pipeline, then handle missing and extreme values in the key columns. Filter to clean- or lien-title listings and engineer three features: `age` (vehicle age at time of listing), `log_odometer` (natural log of odometer), and `in_focal_location` (indicator for your chosen city). Answer the written questions about your filtering choices.

### Part 2: Exploring Your Data
Before fitting anything, look at the variables individually and together. Create a histogram of price and compute summary statistics. Create scatterplots of price vs. raw odometer, price vs. log-odometer, and price vs. age. Answer the written questions about what you observe.

### Part 3: Fitting the Model
Fit the OLS model from the in-class exercise using `smf.ols()`. Examine the summary output and interpret the key coefficients — especially `car_age` and `log_odometer` — in plain English using realistic dollar and mileage values. Discuss R-squared and what it tells you about model fit.

### Part 4: Finding Good and Bad Deals
Compute predicted prices and residuals for every listing. Plot the residual distribution. Flag listings more than 2 standard deviations below the prediction as potential good deals, and listings more than 2 standard deviations above as potentially overpriced. Examine specific listings and consider what the model might be missing.

### Part 5: Reflection
Answer the reflection questions about your prior experience with regression, remaining questions you have, model limitations, and whether you'd actually trust this model if you were car shopping.

---

## Deliverables

When you have completed your work, **follow these steps carefully before submitting**. These will be largely the same on every assignment.

### 1. Clear All Outputs
Before your final submission, you need to clear all cell outputs to ensure a clean starting state:
- In the notebook menu, select **Kernel → Restart & Clear Output** (or **Kernel → Restart Kernel and Clear All Outputs**)
- This removes all previously generated output and resets the kernel

### 2. Run Everything from Top to Bottom
After clearing outputs, verify that your notebook runs correctly from start to finish:
- Select **Run → Run All Cells** (or **Cell → Run All**)
- Watch the cells execute in order
- Ensure there are no errors
- Check that all outputs appear as expected. In particular, **read** your Markdown cells and ensure they look exactly the way you want, just as you would with an essay assignment.

**Why is this important?** This process ensures that:
- Your code doesn't depend on cells being run in a specific order that differs from top-to-bottom
- You haven't accidentally deleted a cell that defines a variable used later
- Someone else (including me, when grading) can view your notebook and see the results. If needed, I can also run the notebook and should see the same results.

### 3. Comment Out Large Outputs (Optional but Recommended)
If any cells print very large DataFrames or long outputs, consider commenting them out or removing the print statements. This keeps your notebook file size manageable and makes it easier to review.

### 4. Commit and Push to GitHub
Once you've verified everything runs correctly:
```bash
git add "Regression.ipynb"
git commit -m "Ready for review"
git push
```
You can also commit by going to the Source Control menu (**View → Source Control** or click on the icon on the left) and using the GUI to do your add-commit-push cycle. Instructions for this are in Module 0 on Canvas.

**Final checklist before submitting:**
- [ ] Kernel restarted and all outputs cleared
- [ ] All cells run successfully from top to bottom
- [ ] All `Q:` questions answered in Markdown cells
- [ ] Large debug outputs commented out or removed
- [ ] Changes committed and pushed to GitHub

---

## AI Policy

You may use AI to *ask questions* if you are stuck or need clarification, and for code completion. Do not use AI to write whole blocks of code and don't copy and paste from a web UI. The purpose of these restrictions is to ensure that you are in the driver's seat on the conceptual pieces of the assignment — particularly the written interpretation questions, which require your own thinking.

---

## Evaluation Criteria

This rubric describes different levels of understanding and skill demonstration. Use it for self-assessment and to understand feedback on your work. Your work will be evaluated more holistically than this rubric implies, but it gives you a sense of what I'm looking for at each facet.

### Code Functionality

**Exemplary**: All code executes flawlessly from top to bottom. All required tasks are completed correctly, including data preparation, feature engineering, model fitting, and residual analysis. The workflow demonstrates clear understanding of the assignment requirements.

**Proficient**: Code executes with only minor issues that don't prevent completion of major tasks. All required tasks are attempted and most are completed correctly. Any errors are minor and don't indicate fundamental misunderstandings.

**Developing**: Code has some execution errors or several tasks are incomplete. Core functionality is present but needs refinement. Some required transformations or visualizations are missing or incorrect.

**Beginning**: Code does not run or has major execution errors. Multiple required tasks are missing or fundamentally incorrect. Demonstrates need for significant additional practice with core concepts.

---

### Data Analysis & Interpretation

**Exemplary**: All analytical questions are answered correctly with clear, data-supported explanations. Demonstrates strong ability to extract meaning from regression output. Coefficient interpretations are specific (using actual dollar and mileage values) and written for a general audience. The good/bad deal analysis is thoughtful and considers model limitations.

**Proficient**: Most questions are answered correctly. Minor errors in interpretation may be present but overall understanding is evident. Answers are supported by the data. Coefficient interpretations may be technically correct but lack real-world grounding.

**Developing**: Some questions are answered incorrectly or incompletely. Demonstrates partial understanding but needs improvement in accuracy or depth. Interpretations may restate the formula rather than translate it into plain language.

**Beginning**: Many questions are unanswered or incorrect. Limited evidence of analytical thinking or ability to interpret regression output. Needs substantial work on connecting model output to meaningful insights.

---

### Finished Product

**Exemplary**: Code is clean, well-organized, and uses best practices. Variable names are meaningful and consistent. Pandas and statsmodels methods are used efficiently and appropriately. Markdown cells are used for commentary and to divide up the workflow. The notebook is easy to read and follow, with proper markdown formatting and logical flow.

**Proficient**: Code is generally clean and readable. Minor inconsistencies in style or efficiency may exist but don't impede understanding. Notebook organization is logical with adequate formatting.

**Developing**: Code works but has readability issues such as unclear variable names, inconsistent formatting, or inefficient approaches. Notebook organization could be improved.

**Beginning**: Code is difficult to read or understand. Poor variable naming, lack of organization, or highly inefficient methods. Minimal attention to presentation or professionalism.

---

### Reflection

In the reflection section, I am looking for thoughtful engagement with the learning process. I seek to learn about your challenges, any insights developed during the assignment, and remaining questions.


