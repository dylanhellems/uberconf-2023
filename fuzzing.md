# Improving Software Fuzzing with AI and ML

Speaker: Justin Reock

- [Improving Software Fuzzing with AI and ML](#improving-software-fuzzing-with-ai-and-ml)
  - [Fuzzing 101](#fuzzing-101)
    - [Limits of QA](#limits-of-qa)
    - [Automated Methods](#automated-methods)
    - [Fuzzing](#fuzzing)
    - [Types of Fuzzers](#types-of-fuzzers)
    - [Limitation](#limitation)
    - [Machine Learning](#machine-learning)
    - [Learn \& Fuzz](#learn--fuzz)
  - [ExploitMeter](#exploitmeter)
  - [Other Resources](#other-resources)
    - [References](#references)

## Fuzzing 101

> "Doctors are the worst patients; coders are the worst testers"

### Limits of QA

- Human cognition has limitations, we can't think of every branch and edge case
- Even if we could think of each and every scenario, our codebases have a lot external libraries and dependencies
- Total hardening of software is virtually impossible
- We needs other non-interactive means of testing our code

### Automated Methods

- Software fuzzing allows us to automatically take an application down as many code paths as possible, even those that we could not determine
- Static code analysis allows us to determine possible code health issues without running it
- Symbolic execution allows us to test a wide range of valid inputs

### Fuzzing

1. Generate inputs
   - Randomized, not just in content but in format and encoding
   - Challenge is to scale down the infinite set of inputs to a reasonable corpus that will generate lots of *interesting* states without too much bias
2. Monitor execution
3. Record *interesting* outputs/states (e.g. exceptions)

### Types of Fuzzers

- Mutation-based
  - Based on modifications to existing valid test cases
  - Generally unbounded, so a lot of corpus data ends up being useless

- Generation-based
  - Based on same input rules that are used to frame the normal test cases
  - Much more bounded than mutation-based
  - Can measure how much of a possible testing surface has been explored

- Evolutionary Fuzzing
  - Applies a bit of learning on top of mutation-based
  - Follows branches of input that generated *interesting* results

### Limitation

- Not a solved problem
- Requires a great deal of software domain knowledge to be effective
  - Is one state actually different than another?
  - Is one input going to generate the same state as another?
  - Is a state *interesting*?
- We run into the same cognitive limitations when we try to derive new ways of mutating input as we do simply deriving the input in the first place

### Machine Learning

- Evolution-based and generation-based fuzzing bear the most promise in terms of ML
- Train a model to predict whether a new generation bit of input will generate an *interesting* state
- Can use existing models to apply predictions to a brand new piece of software
- Areas of focus
  - Reduction in the test corpus
  - Optimized mutation of test corpus
  - Interesting state recognition
  - Bug/vulnerability classification from interesting state
  - Elimination of bias in test corpus (sort of)

### Learn & Fuzz

- RNN to keep track of whether fuzzed input would trigger a previously unknown state
- For the derived data to be useful it must trigger an *interesting* state but not an already known state
- The conclusion of the study was that there still exists tension between learning, which tries to make sense of unordered data by reducing chaos, and fuzzing, which tries to pinpoint various scenarios by increasing chaos

## ExploitMeter

- Combines the accessibility of open source software with deep learning to determine patterns that indicate whether found interesting states are in fact exploitable
- Predicts whether a piece of software is likely to have exploitable vulnerabilities or not, based on the input types that it has learned are exploitable in other open source applications

## Other Resources

### References

- [ClusterFuzz](https://google.github.io/clusterfuzz/)
- [Patrice Godefroid](https://patricegodefroid.github.io/)
- [Learn & Fuzz](https://arxiv.org/abs/1701.07232)
- [Accelerating Software Quality](https://www.perforce.com/resources/accelerating-devops-quality)
- [The Developer Productivity Engineering Handbook](https://gradle.com/developer-productivity-engineering/handbook/)
