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

## Visualisations
visualizations can help users, because humans are generally good at picking up visual paterns. This means that visual representations can help with finding underlying relationships and rules in the data, which may correlate to feature relationships.

It should be noted that visualisations work in a very limited set of dimensions, this means careful selection must be made when choosing what to visiualise.

For linear models with regularisation plots of regression coefficient paths are especially useful. When visualising [[convolutional neural networks]] on image data work has been done on:
- murdoch2019(64,65): filters
- [[murdoch2019]](66): maximally activating responses of individul neurons
- (67): understanding interclass variation
- (68): grouping different neurons

Long Short-Term Memory Networks:
- anaysing state vector (69)
- indentifying individual dimensions corresponding to important features (69)
- tools to track decision process over sequence (70)

### Analysing Trends and Outlier Positions
When interpreting the performance of an ML model, it can also be useful to look at the distribution of predictions and errors.


## Prediction-Level Interpretations
Here, the focus lies on explaining individual predictions made by the model, such a what features and interactions led to the conclusion drawn by the model. Note that prediction-level approaches can sometimes be aggregated to yield dataset-level insights.

## Feature Importance scores
The most popular approach to prediction-level interpretation relies on weiging individual features. This is a minimastion problem. reseach has been performed on this [[murdoch2019]](71-78), with some other methods being researched in [[murdoch2019]](79). Most of the time this boils down to heat-mapping the model's processes.

Despite recent advances is this area, there are concerns about the descriptive accuracy of theme methods. In particular, [[murdoch2019]](80) shows that many popular methods
produce similar interpretations for a trained model versus a randomly initialized one and are qualitatively very similar to an edge detector. Moreover, it has been shown that some feature importance scores for CNNs are doing (partial) image recovery which is unrelated to the network decisions [[murdoch2019]](81).



