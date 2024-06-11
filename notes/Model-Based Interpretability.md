Model based interpretability can be increased by 2 main factors:
- Transparency of model class
- Penetration of Analysis method

The bulk of model-based interpretability is derived from the transparency of the model. Most often this equates to simplicity of the model. In an extreme case, a single-dimensional linear regression problem has a rather easy to interpret resulting model, while [[deep neural networks]] cannot even be described by standard mathematical function descriptions.

# Methodology
## Sparsity
If the data is sparse than the user can also limit the amount on non-zero parameters in the model. This is because sparsity in a data set limits the correlation that can be drawn, and hence it allows for a simpler implementation of a model. There are simply less relations to be learnt.

It is however important to verify the [[model stability]] and [[data stability]] of a model with the implemented sparsity, as these characteristic can be impacted by it.

Because a model is in a more simple form after implementing sparsity it often yields higher descriptive accuracy, while it can increase predictive accuracy at the same time. However, it can also decrease either or both types of accuracy in the [[PDR Framework]].

Lastly, implementations of sparsity must be performed in a targeted manner. It requires an understanding of the data-specific structures, which are impacted by endogenous, as well as exogenous factors. e.g. sample size, type, instrumentation, noise, data corruption, etc.
### Sparsity Methods: ([[murdoch2019]])
- Penalty/Loss Function
	- LASSO
	- Sparse Coding
- Model Selection Criteria:
	- AIC
	- BIC
- subset selection methods
	- Orthogonal Matching Pursuit
- SCAA
Sparsity is often most useful in highly dimensional problems, where the aim is to identify key features for further analysis.

## Simulatability
A model is said to be simulate if a user can internally simulate and reason about its entire decision making process. This is among the stronger constraints to put on a model and can generally be done for small and simple models.

An example of a simulatable model is a [[decision tree]]. Their hierarchical nature makes it easy to run through the logic that the system uses to produce its output.
 Another example is a [[list of rules]].
Simulatable models have a significant descriptive accuracy due to the fact the the IO-response of the model can be determined easily. A persistent issue with simulatable models is their stability (read robustness).

## Modularity
A model is modular if segments of the model can be interpreted in isolation. Modularity can satisfied in varying degrees. [[generalised additive models]] force the relations in a model to be additive and can hence easily be separated. In deep learning, specific methods such as [[attenuation]] and [[modular network architectures]] provide limited insight into a network's dynamics. Stochastic models can be made modular by introducing priors, such that conditionality can be studied.
### *Example*
*When prioritising patient care for patients with pneumonia in a hospital, one possible method is to predict the likelihood of death within 60 d and focus on the patients with a higher mortality risk. Given the potential life and death consequences, being able to explain the reasons for hospitalising a patient or not is very important.*
*A recent study (7) uses a dataset of 14,199 patients with pneumonia, with 46 features including demographics (e.g., age and gender), simple physical measurements (e.g., heart rate, blood pressure), and laboratory tests (e.g., white blood cell count, blood urea nitrogen). To predict mortality risk, the researchers use a generalised additive model with pairwise interactions, displayed below. The variate and pairwise terms $f_j(x_j)$ and $f_{ij} (x_i , x_j )$ can be individually interpreted in the form of curves and heatmaps, respectively:*

$$g(\mathbb{E}[y]) = \beta_0+\sum_{j}f_j(x_j)+\sum_{i\neq j}f_{ij}(x_i,x_j)$$

*By inspecting the individual modules, the researchers found a number of counterintuitive properties of their model. For instance, the fitted model learned that having asthma is associated with a lower risk of dying from pneumonia. In reality, the opposite is true; patients with asthma are known to have a higher risk of death from pneumonia. Because of this, in the collected data all patients with asthma received aggressive care, which was fortunately effective at reducing their risk of mortality relative to the general population.*

## Domain Based Feature Engineering
Domain based feature engineering concerns the way input is used to train a model. Hypothetically one could perfectly fabricate data that is optimal for the learning algorithm to learn the desired dynamics. However, because of the lack of interpretability in most models, this is exactly what we cannot do. Regardless, to some degree a domain expert could review the input data and see if the desired dynamics is abundantly present and if there are no other other dynamics with too much spectral power that might throw the learning algorithm off.

As mentioned before the way that a learning algorithm learns is not trivial and oftentimes stochastic. It is therefore not trivial to determine if feature engineering will impact either, or both, the predictive or descriptive accuracy and how it will do so.

## Model-Based Feature Engineering
Both [[unsupervised learning]] and [[dimensionality reduction]] will yield interpretable features. Both are also automatic ways to do so. Unsupervised methods include clustering, matrix factorisation, and dictionary learning. All these three aim to process unlabelled data and output a description of their composition. dimensionality reduction methods focus on reducing the data to a reduced space, such that it presents itself in a more limited form. In most cases this means that some information is lost, but most of the structure of the data is maintained. However, the reduced features of the data rarely represent anything interpretable to humans and it is thus tricky to use such a method to structure data by the desired features. Methods that can do this include [[principle component analysis]], [[independent component analysis]], and [[canonical correlation analysis]]. However, using these methods some extra steps can be made that will possible yield a few interpretable features.

# Building accurate and interpretable models
**Model Based interpretability is by neture strong at descriptive accurace. Hence, If it can acchieve good predictive accuracy and relevancy, it is preferable.**

**Sometimes model based and [[post-hoc interpretability]] can be combined for better results**.

In cases when model-based interpretability cannot provide good predictive accuracy, the current state of the art requires users to abandon model-based methods. Thus for [[Model-Based Interpretability]] this is the most important direction of research.
promising examples: [[murdoch2019]](7,40,91).

## Tools for feature engineering
More meaningful and informative features can vastly improve a dataset's learnability. Hence, this is likely to yield good descriptive interpretability.  Hence it is important to have tools for exploratory data-analysis. Another important factor is domain knowledge. Tools to enhance these abilities are:
- interactive tools (92-94)
- visualisations (95-97)
- data explaoration tools (98, 99)