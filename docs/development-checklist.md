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

Every Monday morning we hold a *stand-up* meeting, where each team member can review the last week's progress, the current week's goals, and share any issues which are blocking further progress. The meeting is intended to be short and to-the-point, the goal is to share progress and to ensure that issues are raised and discussed within the group. Notes are shared in the #general [slack channel](https://nismod.slack.com/).

### The project's features and bugs are kept in an issue tracker

An issue tracker is a system that is intended to create, update and resolve issues that relate to a certain software package. It helps to keep track of issues and prioritise work. We are aiming to report all issues on Github.

## Is the project well documented?

Writing software documentation is necessary to preserve the valuable information that is often kept in the head of developers. Well documented code is more likely to be reused, extends the lifetime of the application and helps developers in all life-cycle stages of the system.

### There is a README in the project root

A readme is typically the first page read by anyone who is interested in a using or contributing to a coding project. This page acts as a brief overview of the project which includes topics like:

* General description of the project
* Installation instructions
* Build instructions
* Run instructions
* Authors

A template for a `README.md` can be found [on Github](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2).

### There is module- function- and/or method- level documentation

A detailed-level of documentation should provide a deeper understanding of the structure and subfunctions in a coding project. This information is useful to fresh up the knowledge of the original developer, and is essential to anyone new to the project.

A few lines of documentation can already make a big difference in gaining an abstract view of the functionality of certain pieces of software, and avoids the need to read every line of code. Therefore we aim to at least have every module- function and/or method documented in the source code, described with the following information:

* One-line summary of the method/function
* Detailed description of method/function
* List of arguments with pre-conditions
* List of return values with post-conditions

There are standard conventions available to do this, such as:

* Python [Docstrings](https://www.python.org/dev/peps/pep-0257/)

### A `docs` folder contains articles or guides

A documentation folder in the Github repository, is a good place to story any information that is relevant to the coding project. There are tools available that can automatically generate documentation, such as:

* Python: [Sphinx](http://www.sphinx-doc.org)

For webpage style documentation, there are free services available where this can be hosted.

* Host: [Readthedocs](http://readthedocs.org)

### Any corresponding academic paper/s are referenced

## Is the project in version control?

Using a version control system provides benefits in many ways. Collaboration becomes much easier, as source code is shared in the cloud, multiple team members can simultanously work on the same project. Also by saving immediate versions of the source code, it provides us with the possibility to trace back changes and restore to previous versions.

### The current state of the code is accessible to ITRC/nismod developers

We are aiming to host all projects on [github.com/nismod](https://www.github.com/nismod), to ensure the availability of the latest code base to all ITRC/nismod developers.

### There is a history of fairly small, frequent commits with clear messages

Good commit messages are necessary support the reviewing process, it helps to understand *what* was changed and *why* this was necessary. Also it acts as an important input to the release notes, to communicate what has been changed in a certain software revision.

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

Software testing is final step in the development process to discover in which extent a software product meets its specification. Testing is always limited by time or resources, and is a trade-off between the quality of our deliverables. We believe that implementing a basic test strategy will eventually safe us time, therefore we are aiming to adopt the following test principles.

### There is a sanity-check description of how to run the project

**TOM?**

### Integration tests cover large parts of the system, with verifiable outputs

Integration tests covers the complete coding project within its environment. The model is offered a known set of test-data inputs, the model is run and the results are asserted agains a set of test pass values.

### Unit tests cover the majority of implementation details and error cases

Unit testing is a test method by which units of the code are tested individually. Units are tested in procedures that reflect typical and boundary usage. The results are verified agains a set of pass requirements.

### Is the regression testing automated?

Complex software applications can have numerous dependencies and relationships, a small change of code could have an impact on different parts of the software. A typical event is software development is that resolving a bug for one use-case, introduces bugs for other use-cases.

This effect can be avoided by repeatedly carrying out sanity, integration and unit tests. As this is a lot of work by hand, it is usually worth to write an automatic test procedure, there are numerous packages available to help to do this, such as:

Python: [Pytest](https://docs.pytest.org/en/latest/)

If your project is hosted on a public Github repository, it is even possible to automate the executing of tests by using a continuous integration service, such as:

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