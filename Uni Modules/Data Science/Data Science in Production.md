---
tags:
  - Lesson
  - DS_production
---
# Failure is the rule
## Stages
- **Planning**:
	- strategy
	- budget 
	- hiring
	- goals
- **PoC** (proof of concepts):
	- sample
	- EDA
	- Model build
	- Verify
![[Screenshot 2025-02-11 at 13.39.22.png|500]]
- **Production**:
	- regular flow 
	- bias check
	- security
	- govern
	- errors and new trends
	- continuous learning
	- human-machine
	- label drift
![[Screenshot 2025-02-11 at 13.48.26.png|500]]
![[Screenshot 2025-02-11 at 13.50.34.png|400]]
- most of the time it will fail so you need to learn how to fail quickly and cheaply
# Engineering Guarantees for data science
## DataOps
![[Screenshot 2025-02-11 at 14.10.01.png|400]]
1. data validator: scheme conformance and evolution
	- are the types you expect the types they should be
	- also a way to document new features used in the pipeline
2. tests: unit testing, integration testing etc
3. data analyser: basic statistics
	- bias
	- feature/distribution skew
	- defining the distribution and fitting a model
4. Model unit tester: looks fro errors in the training code using synthetic data (schema-led fuzzing)
	- feeding extreme values that are still valid
5. model analysis: be able to explain why decisions are made and that they are still valid
6. Monitoring: Data scientist investigates whats going on with the model
### Tests on features
- **score decomposition**: no clean way to separate influence of a particular incoming node across a non-linear activation like ReLU
	- not really recommended today
- **Ablation Testing**: remove features one at a time, retrain the model and observe the difference in performance $\rightarrow$ Ship-of-Theseus paradox
	- widely used, the main issue being this paradox
- **Feature Permutation**: Examples that never occurred in real life - assume feature independence
	- altering values of a feature, suboptimal as assumes independent features
- **Top-Bottom Analysis**
	- recommended
	![[Screenshot 2025-02-11 at 14.07.26.png|500]]
- feature store means when the next person tries it they don't need to restart the process
### Monitoring
![[Screenshot 2025-02-11 at 14.11.09.png|500]]
## What kind of tests
![[Screenshot 2025-02-11 at 14.11.47.png|400]]
![[Screenshot 2025-02-11 at 14.12.15.png|400]]
- can lead to lots of testing as dimensions increase, expensive and slow
![[Screenshot 2025-02-11 at 14.13.18.png|500]]
- don't run your organisation in excel as a data scientist