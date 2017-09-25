---
title: Development checklist
layout: page
---

This page is intended to provide a short checklist for reference in code review and collaboration.

## Checklist

* TOC

{:toc}

## Are the lines of communication open?

Developing software in a team can be challenging, especially when members are working from different locations throughout the UK. Good cooperation calls for clear goals, information sharing and a common way of working.

### We're keeping in touch productively

Every Monday morning we hold a *stand-up* meeting, where each team member can review the last week's progress, the current week's goals, and any issues which are blocking further progress. The meeting is intended to be short and to-the-point, the goal is to share progress and to ensure that issues are raised and discussed within the group. Notes are shared in the #general [slack channel](https://nismod.slack.com/).

### The project's features and bugs are kept in an issue tracker

An issue tracker is a system that is intended to create, update and resolve issues that relate to a certain software package. It helps to keep track of issues and prioritise work. We are aiming to report all issues on Github.

## Is the project well documented?

Writing software documentation is necessary to preserve the valuable information that is usually kept in the head of developers. Well documented software is more likely to be reused, extends the lifetime of software code and helps developers in all life-cycle stages of a product.

remember later

software useless
reusabality

knowledge transfer
help new users learn quickly

### There is a README in the project root

A readme is typically the first page read by anyone who is interested in a using or contributing to a coding project. This page acts as a brief overview of the project which includes topics like:

* General description of the project
* Installation instructions
* Build instructions
* Run instructions
* Authors

A template for a `README.md` can be found [on Github](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2).

### There is module- function- and/or method- level documentation

A detailed-level of documentation should provide a deeping understanding of the structure and subfunctions of a coding project. This information is useful to fresh up the knowledge of the original developer, and is essential to anyone new to the project.

A few lines of documentation can already make a big difference in gaining an understanding how certain pieces of software works, without having to reverse-engineer each line of code. Therefore we aim to at least have every module- function and/or method, describing the following information in the code comments.

* One-line summary of the method/function
* Detailed description of method/function
* List of arguments with pre-conditions
* List of return values with post-conditions

There are tools available that can use this information to automatically generate document, such as.

* Python [Docstrings](https://www.python.org/dev/peps/pep-0257/)

### A `docs` folder contains articles or guides

Python:

* Generator: [Sphinx](http://www.sphinx-doc.org)
* Host: [Readthedocs](http://readthedocs.org)

### Any corresponding academic paper/s are referenced

## Is the project in version control?

Using a version control system provides benefits in many ways. Collaboration becomes easier, as source code is shared in the cloud, multiple team members can simultanously work on the same project. Also by saving immediate versions of the source code, it provides us with the possibility to trace changes and restore to previous versions.

### The current state of the code is accessible to ITRC/nismod developers

We are aiming to host all projects on [github.com/nismod](https://www.github.com/nismod), to ensure the availability of the latest code base to all ITRC/nismod developers.

### There is a history of fairly small, frequent commits with clear messages

Good commit messages are necessary support the reviewing process, it helps to understand what was changed and why this was necessary. Also it acts as an important input to the release notes, to communicate what has been changed in a certain software revision.

* Write a brief summary of the change in the subject line
* Capitalise the subject line
* Use the imperative mood in the subject line (like these bullet points - start with a verb).
* Explain in the body what has been changed and why this was necessary

### No large or sensitive files are committed (in current state or in history)

Generally, only source code should be kept under version control. Not all files are necessary to keep under version control, such as binaries and model run results. There are also files which strictly should not be uploaded to a (public) repository, such as licensed datasets or database configurations.

Make sure that software changes are 'staged' carefully before executing a commit command. Add a *.gitignore* file to your Github repository to automatically ignore certain folders or file extentions. For [example](https://github.com/nismod/smif/blob/master/.gitignore).

### The project is publicly available under suitable license

Licenses clearly communicate what can and cannot be done with your code.
We encourage you to choose a permissive licenses which doesn't impose unneccessary restrictions on potential users of your code. For example, the MIT license gives permission to any user that they may use, modify and incorporate the code in their own work, but that they must give credit by including the license. A more restrictive license such as GPL effectively disallows commercial use of the code by requiring that all software which uses the code to also be publicly released.

There are various online [guides to choosing a license](https://choosealicense.com).

### If collaborating extensively, features and fixes are developed on branches

Work in branches rather than pushing commits directly in the master
branch. By convention, start the name of a branch with:

* `feature/<feature_description>` for new features
* `bug/<bug_description>` for bug fixes

In git, create a new branch with the command `git branch feature/<feature_description>` and then move to the branch with the checkout command `git checkout feature/<feature_description>`. Alternatively, do both in one command with `git checkout -b feature/<feature_description>`.

## Are there tests?

Software testing is a method to determine to what extent the software meets the requirements.

### There is a sanity-check description of how to run the project

### Integration tests cover large parts of the system, with verifiable outputs

### Unit tests cover the majority of implementation details and error cases

Python:

* [Pytest](https://docs.pytest.org/en/latest/)

### If the project is public, tests are run automatically

Continuous integration service:

* [Travis-CI](https://www.travis-ci.org)

## Is the code well written?

Remember, code is read (like a book) more times that it is written. By using sensible and meaningful names for variables, methods and classes you can ensure that the code is readable.

### Any references to specific file locations are in config files or arguments

The hard coding of file names makes it difficult to deploy your code to another computer.  Best practice is to direct your code to the location of the files by passing in the file path as an argument, or listing the files in a configuration file.

### The code is structured into functions or classes and methods

Functions allow you to reduce duplication of code - a key maxim of good software development is DRY: don't repeat yourself. By keeping code in one place it is easier to maintain, understand and test.

### Names (of packages, modules, functions, methods) are clear

### The code follows a suitable style guide for the language

Within the syntax 'rules' of a compiler, programming languages can be written and structured in a variety of ways. This provides software developers with the freedom to *style* code in the way they prefer or are used to work in. A unified way of styling code becomes increasingly important when a large codebase is shared among multiple members.

A style guide is a set of rules that defines how computer code is styled. Emphasizing on a certain style helps to unify the look and structure of code throughout a project, this improves readability and helps to avoid defects in the software because of misinterpetations. We are aiming to achieve the following code style standards in our development team.

* Python: [PEP 8](https://www.python.org/dev/peps/pep-0008)

Besides that code style is an integral part of a [code review] #code-reviews), this is not well spent time in this stage of the development process. An automatic code quality checker can help to automatically check programming code for deviations from the defined standard. We recommend to use the following tools.

* Python: [pylint](https://www.pylint.org) and [flake8](http://flake8.pycqa.org/en/latest/).  [autopep8](https://pypi.python.org/pypi/autopep8) allows you to automatically apply the PEP8 style to existing code with the command `autopep8 -i my_file.py`