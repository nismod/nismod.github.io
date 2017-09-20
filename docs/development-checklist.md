---
title: Development checklist
layout: page
---

This page is intended to provide a short checklist for reference in code review
and collaboration.

## Checklist
* TOC
{:toc}

## Are the lines of communication open?

Developing software in a team can be challenging, especially when members are
working from different locations throughout the UK. Good cooperation calls for
clear goals, information sharing and a common way of working.

### We're keeping in touch productively

Every Monday morning we hold a stand-up meeting, where each team member can
review the last week's progress, the current week's goals, and any issues
which are blocking further progress. The meeting is intended to be short and to-the-point,
the goal is to share progress and to ensure that issues are raised and discussed
within the group. Notes are shared
in the #general [slack channel](https://nismod.slack.com/).

### The project's features and bugs are kept in an issue tracker

An issue tracker is a system that is intended to create, update and resolve
issues that relate to a certain software package. It helps to keep track of
issues and prioritise work. We are aiming to report all issues on Github.

## Is the project well documented?

### There is a README in the project root

A good README is a short project introduction which might include:

* General description of the project
* Installation instructions
* Build instructions
* Run instructions
* Authors

A template for a `README.md` can be found [on
Github](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2).

### There is module- function- and/or method- level documentation

* Python [Docstrings](https://www.python.org/dev/peps/pep-0257/)

### A `docs` folder contains articles or guides

Python:
* Generator: [Sphinx](http://www.sphinx-doc.org)
* Host: [Readthedocs](http://readthedocs.org)

### Any corresponding academic paper/s are referenced

## Is the project in version control?

Using a version control system provides benefits in many ways. Collaboration
becomes easier, as source code is shared in the cloud, multiple team members can
simultanously work on the same project. Also by saving immediate versions of the
source code, it provides us with the possibility to trace changes and restore to
previous versions.

### The current state of the code is accessible to ITRC/nismod developers

 We are aiming to host all projects on
[github.com/nismod](https://www.github.com/nismod).

### There is a history of fairly small, frequent commits with clear messages

Good commit messages are necessary support the reviewing process, it helps to
understand what was changed and why this was necessary. Also it acts as an
important input to the release notes, to communicate what has been changed in a
certain software revision.

* Write a brief summary of the change in the subject line
* Capitalise the subject line
* Use the imperative mood in the subject line (like these bullet points - start
  with a verb).
* Explain in the body what has been changed and why this was necessary

### No large or sensitive files are committed (in current state or in history)

Not all files are necessary to keep under version control, such as binaries and
model run results. There are also files which strictly should not be uploaded to
a (public) repository, such as licensed datasets or database configurations.
Make sure that software changes are 'staged' carefully before executing a commit
command. Add a *.gitignore* file to your Github repository to automatically
ignore certain folders or file extentions.
[Example](https://github.com/nismod/smif/blob/master/.gitignore)

### The project is publicly available under suitable license

There are various online [guides to choosing a license](https://choosealicense.com)

### If collaborating extensively, features and fixes are developed on branches

Work in branches rather than pushing commits directly in the master
branch. By convention, start the name of a branch with:
- `feature/<feature_description>` for new features
- `bug/<bug_description>` for bug fixes

## Are there tests?

Software testing is a method to determine to what extent the software meets the
requirements.

### There is a sanity-check description of how to run the project

### Integration tests cover large parts of the system, with verifiable outputs

### Unit tests cover the majority of implementation details and error cases

Python:
* [Pytest](https://docs.pytest.org/en/latest/)

### If the project is public, tests are run automatically

Continuous integration service:
* [Travis-CI](https://www.travis-ci.org)

## Is the code well written?

### Any references to specific file locations are in config files or arguments

### The code is structured into functions or classes and methods

### Names (of packages, modules, functions, methods) are clear

### The code follows a suitable style guide for the language

Within the syntax 'rules' of a compiler, programming languages can be written
and structured in a variety of ways. This provides software developers with the
freedom to *style* code in the way they prefer or are used to work in. A unified
way of styling code becomes increasingly important when a large codebase is
shared among multiple members.

A style guide is a set of rules that defines how computer code is styled.
Emphasizing on a certain style helps to unify the look and structure of code
throughout a project, this improves readability and helps to avoid defects in
the software because of misinterpetations. We are aiming to achieve the
following code style standards in our development team.

* Python: [PEP 8](https://www.python.org/dev/peps/pep-0008)

Besides that code style is an integral part of a [code review](#code-reviews),
this is not well spent time in this stage of the development process. An
automatic code quality checker can help to automatically check programming code
for deviations from the defined standard. We recommend to use the following
tools.

* Python: [pylint](https://www.pylint.org) and [flake8](http://flake8.pycqa.org/en/latest/)
