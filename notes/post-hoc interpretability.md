Post hoc interpretability concerns the interpretability of a model after the training has taken place. At this stage the user analyses the trained model to provide additional insights into the model's workings.

Tools to assist in this are:
- basic methods
	- scatter plots
	- histograms
	- salience maps
- Dataset-Level Interpretation (a.k.a. global)
- Prediction-Level Interpretation (a.k.a. local)

# Methodology
Both levels of interpretations provide meaningful insight, and despite being similar, they produce different knowledge. Dataset-level interpretations look at broad scale features of the data to see how these relate to model output, while feature-level interpretations focus on how one specific feature is handled by the model and correlated to one specific prediction. This yields a more fine grained insight.
## Dataset-Level Interpretations
Global interpretations look at the relationships the model has learning holistically, such as visual pasterns, colours, frequency ranges and other high level concepts.
### Interaction and Feature Importance
At the dataset level feature importance scores aim to capture how much an individual feature contributes to a prediction across a whole dataset. This can provide some insight into what features are deemed important to specific predictions by the model. Features can be scored using the following methods:
- murdoch2019(53)
- murdoch2019(54,55)
- [[murdoch2019]](56)

It is also possible to score the interactions between features. Highly nonlinear models such as [[deep neural networks]] are capable of modelling complex interactions between features and hence it is important to know which ones were captured by the model and how much weight is attributed to them. Methods include:
- murdoch2019(21,57)
- murdoch2019(58)
- murdoch2019(59,60)
### Statistical Feature Importance
Sometimes is possible to derive model characteristic from the statistical properties of a model, or the statistics of the data that produces. Especially is the stochastic process is know that produced the training data, the AI model can be seen as a secondary process, transforming the data generator. An example of insight into the model that this might yield is if there are any biases towards certain features of the input data when the model generates its output.
**This method is extremely prone to error and should be used with caution ([[murdoch2019]])**




## Prediction-Level Interpretations
Here, the focus lies on explaining individual predictions made by the model, such a what features and interactions led to the conclusion drawn by the model.