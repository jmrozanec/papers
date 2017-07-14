# Machine Learning: The High-Interest Credit Card of Technical Debt
[Source](https://static.googleusercontent.com/media/research.google.com/es//pubs/archive/43146.pdf)

## Machine Learning and complex systems
Traditional methods of paying off technical debt include refactoring, increasing coverage of unit tests, deleting dead code, reducing dependencies, tightening APIs, and improving documentation. The goal of these activities is not to add new functionality, but to make it easier to add future improvements, be cheaper to maintain, and reduce the likelihood of bugs.
One of the basic arguments in this paper is that machine learning packages have all the basic code complexity issues as normal code, but also have a larger system-level complexity that can create hidden debt. Thus, refactoring these libraries, adding better unit tests

## Complex models erode boundaries
### Entanglements
The most important reason for using a machine learning system is precisely that the desired behavior cannot be effectively implemented in software logic without dependency on external data.
No inputs are ever really independent. We refer to this here as the CACE principle: Changing Anything Changes Everything.
### Hidden feedback loops
Systems that learn from world behavior are clearly intended to be part of a feedback loop. Gradual changes not visible in quick experiments make analyzing the effect of proposed changes extremely difficult, and add cost to even simple improvements.
### Undeclared consumers
Without access controls, it is possible for some of these consumers to be undeclared consumers, consuming the output of a given prediction model as an input to another component of the system. Undeclared consumers are expensive at best and dangerous at worst.
The expense of undeclared consumers is drawn from the sudden tight coupling of model A to other parts of the stack. Changes to A will very likely impact these other parts, sometimes in ways that are unintended, poorly understood, or detrimental. In practice, this has the effect of making it difficult and expensive to make any changes to A at all.
##  Data Dependencies Cost More than Code Dependencies
- unstable data dependencies: some input signals are unstable, meaning that they qualitatively change behavior over time. This can happen implicitly, when the input signal comes from another machine learning model itself that updates over time, or a data-dependent lookup table
- underutilized data dependencies: 
 - legacy Features. The most common is that a feature F is included in a model early in its development. As time goes on, other features are added that make F mostly or entirely redundant, but this is not detected.
 - bundled Features. Sometimes, a group of features is evaluated and found to be beneficial. Because of deadline pressures or similar effects, all the features in the bundle are added to the model together. This form of process can hide features that add little or no value.
 - ǫ-Features. As machine learning researchers, it is satisfying to improve model accuracy. It can be tempting to add a new feature to a model that improves accuracy, even when the accuracy gain is very small or when the complexity overhead might be high.

## System level spaghetti
- glue code: 5% of the code performing ML, 95% of the code requests APIs and exposes ML results via API
- pipeline jungles: Without care, the resulting system for preparing data in an ML-friendly format may become a jungle of scrapes, joins, and sampling steps, often with intermediate files output. Managing these pipelines, detecting errors and recovering from failures are all difficult and costly. Testing such pipelines often requires expensive end-to-end integration tests. All of this adds to technical debt of a system and makes further innovation more costly
- dead experimental codepaths: accumulated workpaths regarding the main one to perform experiments may become expensive to maintain. Should be removed if not used. 
- configuration debt: assertions on configurations are needed in order to prevent mistakes, should be versioned and peer reviewed.

## Dealing with changes from real world
- fixed thresholds in dynamic systems: validate if given thresholds are still useful
- correlations no longer correlate: validate if correlations are spurious or still valid
- monitoring and testing: beware of prediction bias and action limits

## Conclusions: paying it off
Both, engineers and researchers, need to be aware of technical debt. Research solutions that provide a tiny accuracy benefit at the cost of massive increases in system complexity are rarely wise practice. Even the addition of one or two seemingly innocuous data dependencies can slow further progress.

