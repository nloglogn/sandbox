# Graph Structure Estimation

## Prediction of Spatiotemporal Patterns of Neural Activity from Pairwise Correlations
[Marre et al. (2009)](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.102.138101)

### Summary
At first, we observe spikes of Neuron, which correspond to upload pictures to Twitter or Instagram. And we find the joint distribution $P(\{\sigma \}^{t+1};\{\sigma^\prime \}^t)$ which maximizes the entropy $H = -\sum P\log P$. By using Langrange multipliers, we find such distribution and the parameter J including information represents intensity of connection between two nodes. Next, we suppose Markovian hypothesis and existence of stationary distribution. Using this hypothesis, we obtain formulation which has parameters independent on time. Moreover, using formula of conditional probability we reduce the parameter from 7 to 3. Estimation of parameters is done by gradient descent and necessary data --- mean and covariance of spikes --- is calculated by Monte Carlo method.

### Formulation

At first, we consider $N$ people who involved in the fashion trend, and define $\{\sigma_i (t)\}_{i = 1, \dots , N}$ as $\sigma_i (t) = 1$ when $i$-th person uploads a photograph about the item included in the selected category at the time $t$ and $\sigma_i (t) = -1$ otherwise. We denote $\{ \sigma \}^\tau$ as the set $\{ \sigma_1(\tau), \dots , \sigma_N(\tau) \}$. We evaluate the probability distribution $P(\{ \sigma \}^{\tau+1}; \{ \sigma^\prime \}^\tau) = P(\{ \sigma \}^{\tau+1}| \{ \sigma^\prime \}^\tau) P(\{\sigma^\prime \}^\tau)$ which maximizes the "entropy". 

We define $m_i = \langle \sigma_i \rangle$, $C_{ij} = \langle \sigma_i(t) \sigma_j(t) \rangle$, $C_{ij}^\mathrm{1} = \langle \sigma_i(t) \sigma_j(t+1) \rangle$. By using Lagrange multipliers, we find

\begin{equation}
P(\{ \sigma \}^{\tau + 1} ; \{\sigma^\prime \}^\tau) = \frac{1}{Z(\{\sigma\})} \exp \left( \sum_{i=1}^N h_i^\tau \sigma_i^\prime + \sum_{i,j=1}^N J_{ij}^\tau \sigma_i^\prime \sigma_j^\prime + \sum_{i,j=1}^N J_{ij}^{\tau + 1, \tau} \sigma_i \sigma_j^\prime \right) P(\{ \sigma \}^{\tau + 1}), \tag{1}
\end{equation}

where $Z(\{\sigma\})$ is the conditional partition function, and $\{ h_i, J_{ij} \}$ are the Lagrange multipliers corresponding to the constraints given by $\{ m_i, C_{ij} \}$.

Next, we assume that the detailed balance is satisfied for a stationary distribution $P_{\mathrm{stat}}(\{ \sigma \})$. This is the Markovian hypothesis. The Markovian matrix is time-invariant and satisfies

\begin{equation}
P(\{ \sigma^\prime \} | \{ \sigma \}) P_{\mathrm{stat}}(\{ \sigma \}) = P(\{ \sigma \} | \{ \sigma^\prime \}) P_{\mathrm{stat}}(\{ \sigma^\prime \}) \tag{2}
\end{equation}

so that

\begin{equation}
P(\{ \sigma \};\{ \sigma^\prime \}) = P(\{ \sigma^\prime \} | \{ \sigma \}) P_{\mathrm{stat}}(\{ \sigma \}) = \frac{\exp( \sum_{i=1}^N h_i \sigma_i + \sum_{i,j = 1}^N J_{ij} \sigma_i \sigma_j + \sum_{i,j = 1}^N J_{ij}^\mathrm{1} \sigma^\prime \sigma )}{Z(\{ \sigma^\prime\})}P_{\mathrm{stat}}(\{ \sigma^\prime \}), \tag{3}
\end{equation}

where the parameters $J_{ij}$ can be interpreted as barometer of connectedness between $i$-th and $j$-th person. Our ultimate purpose is to estimate this parameters.

We apply the approximation for $Z (\{ \sigma^\prime \})$ up to the second order:

\begin{equation}
\log(Z (\{ \sigma^\prime \})) \approx \log(Z_{\mathrm{eff}}) - \sum_{i=1}^N h_i^r \sigma_i^\prime - \sum_{i,j=1}^N J_{ij}^r \sigma_i^\prime \sigma_j^\prime \tag{4}
\end{equation}

Using this formulation we can write the righ side of the equation (3) as follows:

\begin{equation}
P(\{\sigma\} | \{\sigma^\prime\}) = \frac{1}{Z_{\mathrm{eff}}} \exp \left( \sum_{i=1}^N h_i\sigma_i + \sum_{i,j=1}^N J_{ij} \sigma_i \sigma_j + \sum_{i,j=1}^N J_{ij}^\mathrm{1} \sigma_i^\prime \sigma_j + \sum_{i=1}^N h_i^r \sigma_i^\prime + \sum_{i,j=1}^N J_{ij}^r \sigma_i^\prime \sigma_j^\prime \right) . \tag{5}
\end{equation}

Using the detailed balance, the stationary distribution is also restricted to the second order. $P_\mathrm{stat}$ is represented as follows:

\begin{equation}
P_\mathrm{stat} (\{\sigma\}) = \frac{\exp (\sum{i=1}^N h_i^\mathrm{stat} \sigma_i + \sum_{i,j=1}^N J_{ij}^\mathrm{stat} \sigma_i \sigma_j)}{\sum_{\{ \sigma^{\prime \prime} \} \exp (\sum_{i=1}^N h_i^\mathrm{stat} \sigma_i^{\prime \prime} + \sum_{i,j=1}^N J_{ij}^\mathrm{stat} \sigma_i^{\prime \prime} \sigma_j^{\prime \prime})}, \tag{6}
\end{equation}

where the sum $\sum_{\{\sigma^{\prime \prime}\}}$ is the sum about all the value each elements of the set $\{ \sigma^{\prime \prime}\} = \{ \sigma_1^{\prime \prime}, \dots , \sigma_N^{\prime \prime} \}$ can take.

Furthermore, we note that this equation holds:

\begin{equation}
P_{\mathrm{stat}}(\{\sigma\}) = \sum_{\{ \sigma^\prime \}} P(\{ \sigma \} | \{ \sigma^\prime \}) P_\mathrm{stat} (\{ \sigma^\prime \}). \tag{7}
\end{equation}

The parameters $\{ h_i^\mathrm{stat}, J_{ij}^\mathrm{stat} \}_{i,j=1}^N$ are fully determined by the values of $m_i$ and $C_{ij}$, but we evaluate these parameters using numerical technique.



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
