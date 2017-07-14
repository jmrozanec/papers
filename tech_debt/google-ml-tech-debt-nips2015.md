# Hidden Technical Debt in Machine Learning Systems
[Source](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf)
Notice that concepts in this paper are very similar to the ones outlined in a [previous one](https://github.com/jmrozanec/papers/blob/master/tech_debt/google-ml-tech-debt-nips2014.md) We just highlight new concepts.

## Introduction
Hidden debt is dangerous because it compounds silently.
ML systems have a special capacity for incurring technical debt, because they have all of the maintenance problems of traditional code plus an additional set of ML-specific issues. This debt may be difficult to detect because it exists at the system level rather than the code level. 

## Complex models erode boundaries
## Data Dependencies Cost More than Code Dependencies
## Feedback loops
## ML-System Anti-Patterns
Common Smells. In software engineering, a design smell may indicate an underlying problem in a component or system. We identify a few ML system smells, not hard-and-fast rules, but as subjective indicators.
- Plain-Old-Data Type Smell. The rich information used and produced by ML systems is all to often encoded with plain data types like raw floats and integers. In a robust system,
a model parameter should know if it is a log-odds multiplier or a decision threshold, and a prediction should know various pieces of information about the model that produced it and how it should be consumed.

- Multiple-Language Smell. It is often tempting to write a particular piece of a system in a given language, especially when that language has a convenient library or syntax for the task at hand. However, using multiple languages often increases the cost of effective testing and can increase the difficulty of transferring ownership to other individuals.

- Prototype Smell. It is convenient to test new ideas in small scale via prototypes. However, regularly relying on a prototyping environment may be an indicator that the full-scale system is brittle, difficult to change, or could benefit from improved abstractions and interfaces.

Maintaining a prototyping environment carries its own cost, and there is a significant danger that time pressures may encourage a prototyping system to be used as a production
solution. Additionally, results found at small scale rarely reflect the reality at full scale.

## Configuration debt
Principles of good configuration systems:
- It should be easy to specify a configuration as a small change from a previous configuration.
- It should be hard to make manual errors, omissions, or oversights.
- It should be easy to see, visually, the difference in configuration between two models.
- It should be easy to automatically assert and verify basic facts about the configuration:
number of features used, transitive closure of data dependencies, etc.
- It should be possible to detect unused or redundant settings.
- Configurations should undergo a full code review and be checked into a repository.

## Dealing with changes in external world
## Other Areas of ML-related Debt
- data testing debt: Basic sanity checks are useful, as more sophisticated tests that monitor changes in input distributions.
- reproducibility debt: 
- process management debt: updating many configurations for many similar models safely and automatically, how to manage and assign resources among models with different business priorities, and how to visualize and detect blockages in the flow of data in a production pipeline. Developing tooling to aid recovery from production incidents is also critical. An important system-level smell to avoid are common processes with many manual steps.
- cultural debt:  is important to create team cultures that reward deletion of features, reduction of complexity, improvements in reproducibility, stability, and monitoring to the same degree that improvements in accuracy are valued. In our experience, this is most likely to occur within heterogeneous teams with strengths in both ML research and engineering.

## Conclusions: Measuring Debt and Paying it Off
Useful questions to consider are:
- How easily can an entirely new algorithmic approach be tested at full scale?
- What is the transitive closure of all data dependencies?
- How precisely can the impact of a new change to the system be measured?
- Does improving one model or signal degrade others?
- How quickly can new members of the team be brought up to speed?
