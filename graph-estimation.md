# Graph Structure Estimation

## Prediction of Spatiotemporal Patterns of Neural Activity from Pairwise Correlations
[Marre et al. (2009)](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.102.138101)

### Summary
At first, we observe spikes of Neuron, which correspond to upload pictures to Twitter or Instagram. And we find the joint distribution <img src="/tex/32aa25c96c037c8d016d7c3568c1caae.svg?invert_in_darkmode&sanitize=true" align=middle width=118.60185149999998pt height=26.76175259999998pt/> which maximizes the entropy <img src="/tex/cefc83b228702b7521f1220dbef58e67.svg?invert_in_darkmode&sanitize=true" align=middle width=124.9197774pt height=24.657735299999988pt/>. By using Langrange multipliers, we find such distribution and the parameter J including information represents intensity of connection between two nodes. Next, we suppose Markovian hypothesis and existence of stationary distribution. Using this hypothesis, we obtain formulation which has parameters independent on time. Moreover, using formula of conditional probability we reduce the parameter from 7 to 3. Estimation of parameters is done by gradient descent and necessary data --- mean and covariance of spikes --- is calculated by Monte Carlo method.

### Formulation

At first, we consider <img src="/tex/f9c4988898e7f532b9f826a75014ed3c.svg?invert_in_darkmode&sanitize=true" align=middle width=14.99998994999999pt height=22.465723500000017pt/> people who involved in the fashion trend, and define <img src="/tex/9fb4a831d6a6c8bd1e457c95fa7fe46f.svg?invert_in_darkmode&sanitize=true" align=middle width=102.48743009999998pt height=24.65753399999998pt/> as <img src="/tex/4faba5272a7baf65d07e78a480a22516.svg?invert_in_darkmode&sanitize=true" align=middle width=63.72427379999999pt height=24.65753399999998pt/> when <img src="/tex/77a3b857d53fb44e33b53e4c8b68351a.svg?invert_in_darkmode&sanitize=true" align=middle width=5.663225699999989pt height=21.68300969999999pt/>-th person uploads a photograph about the item included in the selected category at the time <img src="/tex/4f4f4e395762a3af4575de74c019ebb5.svg?invert_in_darkmode&sanitize=true" align=middle width=5.936097749999991pt height=20.221802699999984pt/> and <img src="/tex/e7cf8b1443ee7fc6b03ddf23495c208b.svg?invert_in_darkmode&sanitize=true" align=middle width=76.50970799999999pt height=24.65753399999998pt/> otherwise. We denote <img src="/tex/e2eace78d1aef797f0c77695c95d9ee9.svg?invert_in_darkmode&sanitize=true" align=middle width=33.81349619999999pt height=24.65753399999998pt/> as the set <img src="/tex/944330d14003095e64dbcdf475862fb5.svg?invert_in_darkmode&sanitize=true" align=middle width=135.26109464999996pt height=24.65753399999998pt/>. We evaluate the probability distribution <img src="/tex/49f3ff5cc300e13978b6369ad8149260.svg?invert_in_darkmode&sanitize=true" align=middle width=330.956736pt height=26.76175259999998pt/> which maximizes the "entropy". 

We define <img src="/tex/1e1cc54b8481374bba6287c2b35bdc4f.svg?invert_in_darkmode&sanitize=true" align=middle width=69.47486534999999pt height=24.65753399999998pt/>, <img src="/tex/7f5f8c352e7f3ce9a2be7c37aa68abec.svg?invert_in_darkmode&sanitize=true" align=middle width=126.65767124999999pt height=24.65753399999998pt/>, <img src="/tex/75e26ecf8b29271112186ec9469666d5.svg?invert_in_darkmode&sanitize=true" align=middle width=154.96807094999997pt height=26.76175259999998pt/>. By using Lagrange multipliers, we find

<p align="center"><img src="/tex/f3be98a1be2727f13e4c759c9d6b966a.svg?invert_in_darkmode&sanitize=true" align=middle width=681.4927316999999pt height=59.1786591pt/></p>

where <img src="/tex/0b987474b367129840d6f0b5916552cd.svg?invert_in_darkmode&sanitize=true" align=middle width=51.60400244999999pt height=24.65753399999998pt/> is the conditional partition function, and <img src="/tex/8cafb30d4e8dcc4fb0f97bf1a0f4e443.svg?invert_in_darkmode&sanitize=true" align=middle width=59.38079399999999pt height=24.65753399999998pt/> are the Lagrange multipliers corresponding to the constraints given by <img src="/tex/b468f6fb3ba84832bb3a9c8cec094920.svg?invert_in_darkmode&sanitize=true" align=middle width=66.97633139999998pt height=24.65753399999998pt/>.

Next, we assume that the detailed balance is satisfied for a stationary distribution <img src="/tex/4872d4b65e54f44a338896da1a523525.svg?invert_in_darkmode&sanitize=true" align=middle width=72.61666005pt height=24.65753399999998pt/>. This is the Markovian hypothesis. The Markovian matrix is time-invariant and satisfies

<p align="center"><img src="/tex/a7222f2c7d777f4ca0ce0f476b450416.svg?invert_in_darkmode&sanitize=true" align=middle width=523.66118475pt height=17.2895712pt/></p>

so that

<p align="center"><img src="/tex/049549884831a0fbe03b03c9aa6e5aca.svg?invert_in_darkmode&sanitize=true" align=middle width=731.89848765pt height=63.1755498pt/></p>


### Limitation
We must suppose Markovian hypothesis. Thus, the propagation process must be dependent only on the current status.
Whether Markovian hypothesis is fulfilled depends on our situation and solution. Our purpose is to investigate the trend. Trend itself doesn't have Markovian property, but some techniques might allow our situation to fit Markovian.

### Amount of computational time
O(2^N) occurs when reducing the parameters, because the sum is about all the condition of {σ'}. It seems not be able to be avoided by Monte Carlo method or other statistical algorithms.

### Implimation Difficulty
Hard. It is because there are complicated processes in reducing parameters, and because there are no explanation about gradient descent and Monte Carlo integration. It seems to be necessary to ask the authors directly.

### Output
Joint distribution about spikes of current and next time. In addition, we can find the some information about connectedness of each node.

### Input
Upload event for each times.

### Amount of data that memory will have
Huge. It is because we have to solve O(2^n) size equation during reduction of parameters.

### Accuracy
Accuracy is not noted in the paper.
