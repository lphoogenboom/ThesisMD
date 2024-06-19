---
aliases: LIME
---
[[LIME]] was first introduced in 2016 by Ribeiro et al. The main focus of LIME is to look at each prediction separately and form a interpretable local model around each datum. This forms a submodular optimisation problem. The goal of this is to be able to form explainable interpretations of any classifier in any process or model.

in this problem they look at data locally and formulate a model that forms a combined loss $\mathcal{L}$ function of the global loss function $f(x)$ and and loss on a simply interpretable local function $g(x)$. The total loss is minimised using the function description of $g(x)$ as a minimisation variable in the set $G$ of simple functions. The term $\Omega(g)$ is a complexity measure, causing the minimisation function to yield the simplest local model $g(x)$ among the ones with the best loss.

$$\xi(x) = \arg\min_{g\in G} \mathcal{L}(f,g,\pi_x)+\Omega(g)$$
The paper [[Ribeiro2016]] claims that the novel technique explains the predictions of **any** classifier in an interpretable and faithful way. This is a bold claim. 

# Interpretable Data Representations
An explanation needs to be interpretable. I.e. There needs to be a formulation of the reason the model return a certain output that is fathomable by humans. It is important that both the scale and complexity are at a human level. It is unlikely that a human will correlate hundreds of thousands of factors and at the same time it is also unlikely that a human will be able to track highly non-convex relations. Hence, we would like to see a simple representation of the data with straightforward relations.

Examplese of these can be word embeddings, binary vectors, and visualisations.

# Fidelity-Interpretability Trade-off
In order to conduct LIME we will consider an explanation as a model $g\in G$, where $G$ is the set of all local models. The model we are trying to explain can be denoted as $f:\mathbb{R}^d \mapsto \mathbb{R}$. $\pi_x(z)$ functions as a proximity measure between $z$ and $x$, with $x$ being the model output.  We can hence formulate a $\mathcal{L}(f,g,\pi_x)$ such that $\mathcal{L}$ represents the unfaithfulness of the local estimator $g$ with respect to $f$.  Hence in minimising $\mathcal{L}$ and $\Omega$ we optimise the local fidelity and complexity of $g$.
$$\xi(x) = \arg\min_{g\in G} \mathcal{L}(f,g,\pi_x)+\Omega(g)$$
# Sampling for Local Exploration
Because the explained needs to be model agnostic, we need to not make any assumptions about $f$; We need any $f$ to be viable. In order to estimate the local behaviour of $f$, multiple samples can be drawn around it. These samples are weighted with $\pi_x$, such that their proximity is taken into account when forming a local estimator. [[Ribeiro2016]] suggests that these samples should be drawn uniformly around $x'$.  These samples include only a fraction of the non-zero information in $x$', forming $z'$.

