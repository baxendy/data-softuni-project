# Talking to Your Data

## When should a BI assistant ask a clarifying question? A simple Bayes–Shannon model tested on AdventureWorks

Business-intelligence assistants let people ask questions about their data in plain language, but the questions are often ambiguous: *show sales by region* does not say whether "sales" means money or units, which level of geography is meant, or which period. This project builds a small mathematical model of the conversation between a user and a BI assistant and tests it with simulated requests on Microsoft's AdventureWorksDW sample data warehouse:

1. **Combinatorics**: count the possible interpretations of a request (rule of product).
2. **Probability**: estimate their probabilities with Bayes' theorem and a Naive Bayes classifier.
3. **Information theory**: measure the uncertainty of the assistant with Shannon entropy.
4. **Decision rule**: ask a clarifying question while the entropy is above a threshold τ.

## Main results (480 test requests, seed 0)

| | without semantic layer | with semantic layer |
|---|---|---|
| Possible interpretations *N* | 432 | 144 |
| Mean initial uncertainty | 8.37 bits | 3.87 bits |
| Accuracy, no questions | 9.8% | 50.0% |
| Accuracy, entropy rule τ = 1 bit | 68.8% | 91.0% |
| Mean questions, τ = 1 bit | 3.00 | 2.16 |

* All four hypotheses are supported: the semantic layer lowers the uncertainty (H1) and the number of questions (H4), uncertainty goes together with wrong answers (H2), and questions raise accuracy (H3). All tests stay significant after a Bonferroni correction, and the direction of all four holds in 20 of 20 repetitions with new random requests.
* A surprise: for the accuracy of the final answer, a threshold on the probability of the most likely interpretation works better than the entropy rule (mean accuracy for a budget of 0–2 questions: 0.720 against 0.680 with the semantic layer, 0.291 against 0.216 without it).

## Mathematics used

| Area | What is used |
|---|---|
| High-school maths | logarithms (log₂), sum and product notation |
| Probability and combinatorics | rule of product, Bayes' theorem, independence, random variables, simulation with a seed |
| Statistics | mean, standard deviation, histogram and box plot, confidence intervals (central limit theorem), Wilcoxon, Mann–Whitney and McNemar tests, Bonferroni correction |
| Calculus | the area under a curve with the trapezoidal rule |

## How to run

1. Install [Anaconda](https://www.anaconda.com/download) (Python 3.14.6). The results were produced with NumPy 2.5.3 and SciPy 1.18.1.
2. Download the data as described in [`data/README.md`](data/README.md).
3. Open `DataProject.ipynb` (for example in VS Code with the Jupyter extension and the Anaconda `base` kernel) and run all cells.

## Repository structure

```
DataProject.ipynb   the notebook: maths, data, simulation and results
data/README.md      where to download the AdventureWorksDW files
```

## Data

AdventureWorksDW is Microsoft's official sample data warehouse (Microsoft SQL Server Samples, MIT License). The notebook reads the sales territories and the internet sales from two of its CSV files. The user requests are simulated by the notebook; all their frequencies are listed in the notebook as assumptions.
