---
title: Development practices
layout: page
---

This page offers a brief overview of software development practices,
which are intended to define a standard way of working within the ITRC Mistral
project. The goals of these standard practices are to facilitate collaboration,
achieve a high quality of product and to support future developers and users
throughout the life cycle of NISMOD-2.

Please feel free to make any changes or additions to this document, but discuss deviations from the standard way of working with members of the team.

* TOC
{:toc}

## Coding style
Within the syntax 'rules' of a compiler, programming languages can be written and structured in a variety of ways. This provides software developers with the freedom to *style* code in the way they prefer or are used to work in. A unified way of styling code becomes increasingly important when a large codebase is shared among multiple members.

### Style guides
A style guide is a set of rules that defines how computer code is styled. Emphasizing on a certain style helps to unify the look and structure of code throughout a project, this improves readability and helps to avoid defects in the software because of misinterpetations. We are aiming to achieve the following code style standards in our development team.

* C#: [C# style guide]()
* Java: [Java style guide]()
* Python: [PEP 8](www.python.org/dev/peps/pep-0008)

### Quality checker
Besides that code style is an integral part of the [code review](#review), this is not well spent time in this stage of the development process. An automatic code quality checker can help to automatically check programming code for deviations from the defined standard. We recommend to use the following tools.

* C#: [C# quality checker]
* Java: [Pylint](www.pylint.org)
* Python: [Python quality checker]

## Collaborating
Developing software in a team can be challenging, especially when members are working from different locations throughout the UK. Good cooperation calls for clear goals, information sharing and a common way of working. 

### Stand up
Every Monday morning we hold a *stand up* meeting, where each team member gets the opportunity to share the progress that has been made over the past week, the activities that are planned for the next week and which issues are blocking items to progress further. The meeting is intended to be short and to-the-point, the goal is to share progress and to ensure that issues are raised and discussed within the group. Every meeting is seated by a chairholder and notes are shared via the #general channel of [slack](http://nismod.slack.com/).

### Issue tracking
An issue tracker is a system that is intended to create, update and resolve issues that relate to a certain software package. It helps to keep track of issues, distribute assignments and priotitize work. We are aiming to report all issues on the [Github](www.github.com) issue tracking system.

### Version Control
Using a version control system provides benefits in many ways. Collaboration becomes easier, as source code is shared in the cloud, multiple team members can simultanously work on the same project. Also by saving immediate versions of the source code, it provides us with the possibility to trace changes and restore to previous versions. We are aiming to host all projects on [Github](www.github.com).

#### Commit Messages
Good commit messages are necessary support the reviewing process, it helps to understand what was changed and why this was necessary. Also it acts as an important input to the release notes, to communicate what has been changed in a certain software revision.

* Write a brief summary of the change in the subject line
* Explain in the body, what has been changed and why this was necessary

#### Size of Commits

#### Branch vs. Master
Work in feature/bug branches rather than pushing commits directly in the master branch. Include 

Start the name of a branch with:
* *feature/<feature_description>* for new features implementations
* *bug/<bug_description>* for bug fixes

#### Code reviews<a name="review"></a>

#### Repository contents
Not all files are necessary to keep under version control, such as binaries and model run results. There are also files which strictly should not be uploaded to a (public) repository, such as licensed datasets or database configurations. Make sure that software changes are 'staged' carefully before executing a commit command. Add a *.gitignore* file to your Github repository to automatically ignore certain folders or file extentions. [Example](https://github.com/nismod/smif/blob/master/.gitignore)

## Documentation
Good software does not need documentation? Unfortunatelly 


### Summary
A Github project description should be written that describes at least:

* General description of the project
* Installation instructions
* Build instructions
* Run instructions
* Authors

A template for a good README.md can be found [on Github](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2).

### Technical documentation


Python:
* Style: [Docstrings](www.python.org/dev/peps/pep-0257/)
* Generator: [Sphinx](www.sphinx-doc.org)
* Numpy Extension: [Numpydoc](http://pypi.python.org/pypi/numpydoc?)
* Host: [Readthedocs](http://readthedocs.org)

Java: 
* Javadoc?

### License for public
As public GitHub repositories are accessible by anyone on the internet, it is important to include a license in the repository overview. 

We prefer the use of the following licences:
* (for Open-source projects)
* (for .... projects)

## Testing
Software testing is a method to determine to what extent the software meets the requirements. 
### Unit testing

### Integration testing

Python 3: 
* [Pytest](www.pytest.org)

Java:

### Deployment

Public projects: 
* [Travis-CI](www.travis-ci.com)

Private projects: ?


## Development Stack
The development stack refers to the preferred set of applications, tools and libraries that we use throughout the development team.

### Environment
All: [Vagrant](www.vagrantup.com)

### Coding 
Python: 
* [Standard Library](https://docs.python.org/3/library/index.html)
* [Numpy & Scipy](https://docs.scipy.org/doc/)

Java:

## Further reading

Wilson G, Bryan J, Cranston K, Kitzes J, Nederbragt L, et al. (2017) Good enough practices in scientific computing. PLOS Computational Biology 13(6): e1005510. [Link](https://doi.org/10.1371/journal.pcbi.1005510)

Wilson G, Aruliah DA, Brown CT, Chue Hong NP, Davis M, et al. (2014) Best Practices for Scientific Computing. PLOS Biology 12(1): e1001745. [Link](https://doi.org/10.1371/journal.pbio.1001745)
