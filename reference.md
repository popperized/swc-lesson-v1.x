---
layout: reference
root: .
---

## Summary of Basic Popper Commands

  * `init`. Initialize a Popper project or pipeline.
  * `run`. Run one or more pipelines and report on their status.
  * `search`. Search existing pipelines (stored on Github) by 
    providing a keyword.
  * `ci`. Generate CI service configuration files.

These are executed by executing `popper <cmd>`, where `<cmd>` is any 
of the commands listed above. For more, type `popper --help` on your 
terminal.

## Glossary

DevOps
:   A term used to refer to modern software delivery practices. The 
definition we use throughout this lesson is the one from [Bass et al. 
2015](https://books.google.com.mx/books?id=fcwkCQAAQBAJ): "a set of 
practices intended to reduce the time between committing a change to a 
system and the change being placed into normal production, while 
ensuring high quality".

pipeline
:   A list of sequential [stages](#stage) representing an end-to-end 
scientific exploration. See 
[here](https://popper.readthedocs.io/en/latest/sections/examples.html) 
for examples.

stage
:   A stage represents an item in a pipeline in charge of doing one or 
more tasks. In Popper, a stages corresponds to a Bash script and a 
task is an invocation to built-in Bash commands or external tools such 
as Python, Docker, etc.

convention
:   A set of commonly-agreed high-level guidelines.

OSS
:   Open-source software.

continuous integration
:   A software development methodology for continuously testing 
changes to a software codebase.

CI
:   See [continuous integration](#continuous_integration)

## External References

  * [Popper official documentation](https://popper.rtfd.io).
  * [Periodic table of DevOps 
    tools](https://xebialabs.com/periodic-table-of-devops-tools).
