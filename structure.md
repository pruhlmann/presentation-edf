# FMCPE Idea flow

## Intro SBI : Paremeter estimation

- Present the idea of parameter estimation
    - Characterize models by a set of parameters, forward modeling
    - Inverse problems
    - Examples: 
- Likelihood free inference vs Bayesian inference
    - Likelihood is the bottleneck
    - Simple solution : Use samples instead
- Main SBI approaches : 
    - ABC --> Most intuitive 
    - Neural methods (NPE) --> Give some details on NPE training ? They allow to estimate uncertainties
- Challenges and limitations in SBI: Data efficiency, overconfident posterior with neural methods (overfit), **model misspecification** $\rightarrow$ Example from Cannon 2022.

## Misspecfication under the scope of multi-fidelity

- Introduction to mm, different sources of misspecification : 
    - Simplified physics
    - Discretization / numerical errors
    - Measurment noise or partial observation (eg Medical imaging)

- Effect on SBI methods
    - Neural methods are most affected due to the distribution shift

- How we approach model misspecification
    - Different ways to represent the DGP.
        - $\theta \rightarrow x \rightarrow y$
        - $\theta \rightarrow y \rightarrow x$
        - $\theta \rightarrow x$ and $\theta \rightarrow y$ **Focus on this one**
    - Our approach is agnostic to the true DGP
    - Motivation to using a calibration set (eg multifidelity), how do we obtain the data, ground truth measurement or from a costly simulator ?

- Stress that we don't focus our effort on reducing the overall cost, but rather have the best posterior estimate possible given a budget

## Correcting the posterior with high fidelity data
- Details on FMPE (Not sure where to put it) --> Maybe not
- Present pevious work (RoPE, MF-NPE), other methods such as RNPE, NPE-RS --> **in appendix** 
- Motivate our approach, 3 main points
    - We use FM to generate samples from $p(\theta | y)$, we need a better source than a gaussian --> Use a figure to illustrate
    - Designed a simulation-informed source $\pi(\theta | y)$ that is closer to the target posterior $p(\theta|y)$
    - We chose a source of the form
           $$ \pi(\theta |y) = \int p(\theta|x)q(x|y)dx $$
      And learn $q(x|y)$ with $(S(\theta_i),y_i)$
      
    - Joint optimization for more robustness

## Results / limitations / Future works

- Show main results + ablation
- Present the causal chambers dataset
- Limitations:
    - Methods is more costly than basics NPE
    - Sensible to training hyperparameters at low calibration sizes (early stopping)
    - Yet to be applied to large scale simulators
- Future work : 
    - Optimal source choice
    - More than 2 fidelity levels
    - Faster training with Distillation and/or better sampling schemes
    
- SBI Hackathon in January :+1: 