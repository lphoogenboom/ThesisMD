The PDR desiderata concern 3 main factors that impact interpretability in machine learning:
- Predictive Accuracy
- Descriptive Accuracy
- Relevancy

# Accuracy
Accuracy in machine learning interpretability refers to the idea that the learned model is true to the thought process the underlies its function. In other words, a model needs to fit itself to the intended purpose, rather than fitting itself to other dynamics that happen to produce good results.
## Predictive Accuracy
The ability of a model to learn the underlying relations in the data is characterised by predictive accuracy. If there is a high predictive accuracy, the model will draw the right correlations and will therefor be able to be applied more agnostically by the end user. test-set accuracy is a common measure of predictive accuracy. Here, the idea is that the data is different, but the correlations still hold. Hence, if the model is trained properly, it will be able to process the data correctly despite having never encountered it before.
## Descriptive Accuracy
There is also a form of accuracy that comes into play in post-hoc analysis. Because of the black-box nature of e.g. [[deep neural networks]], the post-hoc analysis performed on such models often misrepresents the learnt relations in the data. Descriptive accuracy can thus be impacted by 2 main factors:
- Transparency of the model class
- Ability of analysis tools to uncover learnt relations
## Predictive vs. Descriptive Accuracy
Oftentimes, there is a trade off to be made between either forms of accuracy in the selection of a model class. Model-based descriptions of models generally tend to yield higher descriptive accuracy ([[Model-Based Interpretability]]), because in their nature they tend to better uncover the inner workings of a model. However, more complex tasks require more complex models, which in turn often are more opaque. Therefore, in order to achieve higher predictive accuracy it is often required to sacrifice descriptive accuracy.

# Relevancy
What is sometimes not trivial is the assessment of the relevance of the learned model. A model can accidentally be trained to extract data that is not relevant to the user. Different users can have different interests in the same data and it is therefore important to keep in mind the relevancy of the model in question.
### Definition
*We define an interpretation to be relevant if it provides insight for a particular audience into a chosen domain problem.*

# Measuring Interpretation Desiderata
The exists no clear consensus around how to evaluate interpretation methods. Some ground laying work has been done [[murdoch2019]](12-14). The standards of evaluations vary between different source, which makes it hard to research and implement suitable methods.

In order to combat the the PDR framework demands at least an improvement on one of the desiderata without detriment to the other desiderata. Predictive accuracy improvements are easily measured, be the other desiderata remain an issue.
## Measuring Descriptive accuracy
Measuring an improvement in what a model has learnt through its output would be to improve the descriptive accuracy of an interpretation. Descriptive accuracy is notoriously hard to qualify [[murdoch2019]](82). Often researcher will often cherrypick interpretations on a limited set of features that seem reasonable, but this hardly says anything about the model at the scale of a dataset. Hence, one should not want to do this.

The current state of the art is not clear on a standard benchmark, but there have been some promising movements. In particular the use of [[simulation studies]] could be a partial solution ([[murdoch2019]](59,89,21)).

# Demonstrating Relevancy in Real-World Problems
It is also suprisingly non-trivial to improve interpretation methods for relevancy. This can be done through heatmaps, rationales, feature hierarchies, identifying important elements in the training set, etc.

There have been 2 main way of showing improved relevancy:
- Using an interpretation to solve a domain problem (strongest) ([[murdoch2019]](21))
- Human surveys can also be used to study the relevance to users withing the context of a specific domain (e.g. image processing for clinicians)