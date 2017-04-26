---
title: A short introduction to Git
layout: presentation
---

# Computational Science Seminar

### A short introduction to version control with Git

Tom Russell & Will Usher

---

# Agenda

1. intro (Will)
1. concepts (Tom)
1. live coding (Both)
1. summary (Tom)
1. next steps (Will)

---

## Introduction

* Given the very limited time we can only give you a flavour of version control

* Version control and *git* has a steep learning curve

* There are many resources for self learning
  * Software Carpentry
  * Courses within the University of Oxford
  * The Research Support team in SOGE

---

## Resources

These slides are available from:
- https://nismod.github.io/git-novice/presentation/

Further resources are available from the website:
- https://nismod.github.io/git-novice/

A list of commands used in the session is available for quick reference:
- https://nismod.github.io/git-novice/commands/


---

## Concepts


---

## Live Coding


---

## Summary


---

## Automate your workflow

* Repetition - bad
* Automation - good
  * e.g. write a script to fetch data, run analysis and draw graphs
* Make research reproducible and auditable

```
$ my_model --version
98d2
$ fetch_dataset(53dl)
dataset_53dl
$ run_model(dataset_53dl)
results_2017_04_13_53dl_98d2
$ create_graphs(results_2017_04_13_53dl_98d2)
```

---

## Write Tests

* Regression Tests
  * Does my model give the same results as last time with the same data?
* Functional Tests
  * Does my model produce the result in the way I want, when I give it a dataset?
* Unit Tests
  * Does `fetch_dataset` fetch `dataset_53dl` when passed the argument `53dl`?

---

## Use Version Control

