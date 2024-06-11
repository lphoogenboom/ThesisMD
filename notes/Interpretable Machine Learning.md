Interpretation of an ML model refers to the extraction of information from them. Generally this concerns meta-information, rather than model parameters. In other words, interpretability rather concerns the learned cognition than the actual anatomy of a model.

Interpretation methodology can be implemented at every stage of machine learning. This can concern anything from preprocessing of the training data, to finding domains in which the output can be easily analysed by human (e.g. visualisations). 

There is one main distinction in interpretability methodology; [[Model-Based Interpretability]] and [[post-hoc interpretability]]. Either methods are explained on their own pages. The quality of methods can be judged along the [[PDR Framework]]. This framework concerns three main desiderata:
- Predictive Accuracy
- Descriptive Accuracy
- Relevancy
See the [[PDR Framework]] for more info on these desiderata.
# [[Model-Based Interpretability]]
Model based interpretability can be increased by 2 main factors:
- Transparency of model class
- Penetration of Analysis method

The bulk of model-based interpretability is derived from the transparency of the model. Most often this equates to simplicity of the model. In an extreme case, a single-dimensional linear regression problem has a rather easy to interpret resulting model, while [[deep neural networks]] cannot even be described by standard mathematical function descriptions.
# [[post-hoc interpretability]]
Post hoc interpretability concerns the interpretability of a model after the training has taken place. At this stage the user analyses the trained model to provide additional insights into the model's workings.

Tools to assist in this are:
- basic methods
	- scatter plots
	- histograms
	- salience maps
- Dataset-Level Interpretation (a.k.a. global)
- Prediction-Level Interpretation (a.k.a. local)
