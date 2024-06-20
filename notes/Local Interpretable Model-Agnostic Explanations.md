---
aliases: LIME
---
[[LIME]] was first introduced in 2016 by Ribeiro et al. The main focus of LIME is to look at each prediction separately and form a interpretable local model around each datum. This forms a submodular optimisation problem. The goal of this is to be able to form explainable interpretations of any classifier in any process or model.

in this problem they look at data locally and formulate a model that forms a combined loss $\mathcal{L}$ function of the global loss function $f(x)$ and and loss on a simply interpretable local function $g(x)$. The total loss is minimised using the function description of $g(x)$ as a minimisation variable in the set $G$ of simple functions. The term $\Omega(g)$ is a complexity measure, causing the minimisation function to yield the simplest local model $g(x)$ among the ones with the best loss.

$$\xi(x) = \arg\min_{g\in G} \mathcal{L}(f,g,\pi_x)+\Omega(g)$$
The paper [[Ribeiro2016]] claims that the novel technique explains the predictions of **any** classifier in an interpretable and faithful way. This is a bold claim. 

# Interpretable Data Representations
An explanation needs to be interpretable. I.e. There needs to be a formulation of the reason the model return a certain output that is fathomable by humans. It is important that both the scale and complexity are at a human level. It is unlikely that a human will correlate hundreds of thousands of factors and at the same time it is also unlikely that a human will be able to track highly non-convex relations. Hence, we would like to see a simple representation of the data with straightforward relations.

Examples of these can be word embeddings, binary vectors, and visualisations.

# Fidelity-Interpretability Trade-off
In order to conduct LIME we will consider an explanation as a model $g\in G$, where $G$ is the set of all local models. The model we are trying to explain can be denoted as $f:\mathbb{R}^d \mapsto \mathbb{R}$. $\pi_x(z)$ functions as a proximity measure between $z$ and $x$, with $x$ being the model output.  We can hence formulate a $\mathcal{L}(f,g,\pi_x)$ such that $\mathcal{L}$ represents the unfaithfulness of the local estimator $g$ with respect to $f$.  Hence in minimising $\mathcal{L}$ and $\Omega$ we optimise the local fidelity and complexity of $g$.
$$\xi(x) = \arg\min_{g\in G} \mathcal{L}(f,g,\pi_x)+\Omega(g)$$
# Sampling for Local Exploration
Because the explained needs to be model agnostic, we need to not make any assumptions about $f$; We need any $f$ to be viable. In order to estimate the local behaviour of $f$, multiple samples can be drawn around it. These samples are weighted with $\pi_x$, such that their proximity is taken into account when forming a local estimator. [[Ribeiro2016]] suggests that these samples should be drawn uniformly around a point $x$. However, a simplification $x'\in\{0,1\}^{d'}$ of $x$ is used. Hence we also draw samples $z'\in\{0,1\}$. $z'$ only contains a fraction of the nonzero elements of $x'$. Using the model $z\in \mathbb{R}^d$ can be retrieved from $z'$. 

## Sparse Linear Explanations
[[Ribeiro2016]] limits itself to $G$ only containing linear functions and used a proximity measure $\pi_x(z)=e^{\frac{-D(x,z)^2}{\sigma^2}}$ Where the distance function $D$ depends on the type of data. e.g. [[cosine distance]], [[L2 distance]]. The local loss was defined as below.

$$\mathcal{L}(f,g,\pi_x) = \sum_{z,z'\in\mathcal{Z}}\pi_x(z)(f(z)-g(z'))$$
Moreover, the complexity measure was defined as
$$\Omega(g)=\infty\mathbb{1}[||w_g||_0>K]$$
In the case of [[Ribeiro2016]] there was a language classification, but this formulation can also work for imaging. In this case the function would work with [[super-pixels]], which can be determined with any arbitrary method. $K$ signifies a maximum complexity. 

Something about [[LASSO]] and [[K-LASSO]]. In practice it can all be quite fast...

# Submodular Picking for Explaining Models
It is not sufficient to assess trust in the global model if just a couple local predictors are assessed. A multitude of explanations can certainly be insightful, but the chances are low that some randomly picked ones will have a good pallet of qualities to gain insight in the function of the model. Hence it would be nice to arithmetically select a subset of interpretations to present to the user that will actually further the user'as insight. This is exactly what we will do

## Pick step
Suppose we can characterise a user's patience $B$ by stating the amount of interpretations they will analyse. These interpretations then need to be selected from the set of all interpretations $X$.

We can then setup a pick step where we will select the optimal interpretations to add insight for a user's patience. In order to this we want to select a diverse set of interpretations in terms of the used features and predictions. i.e. **non-redundance**.

If $|X|=n$ we can form a matrix $W\in\mathbb{W}^{n\times d'}$ with $\mathbb{W}$ being a matrix containing all explanations as rows and interpretable components as columns. The values in the matrix are the importance weights $|w_{g_{ij}}|$, which denote the importance of an interpretable feature in an explanation. 

By looking at the magnitudes of each column we can see how important a feature is in the global explanation space (i.e. how much of a role it plays over all explanations). This importance measure if called $I_j = \sqrt{\sum^{n}_{i=1}W_{ij}}$. In the example of figure 5 in [[Ribeiro2016]] it would be expected that the second feature is the most important, given that it uses a binary encoding. Hence we would expect this one to appear in $W$ even with a budget $B$ of 1.

