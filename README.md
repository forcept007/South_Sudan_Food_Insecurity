# South Sudan Project 
In South Sudan, where over 2/3 of the population face food insecurity, the scars of the South Sudanese Civil War (2013-2020) persist, marked by conflicts between liberation movements and governments, including Sudan's People Liberation Movement (SPLM) and Sudan People's Liberation Movement-in-Opposition (SPLM-IO), along with various rebel groups (Aufiero, P. (2021). "South Sudan at a Crossroads."
Human Rights Watch). The ever-changing dynamics of power and conflict in this region pose a continuous threat of severe, unforeseen hunger (Oxfam International. (n.d.). "Hunger Crisis in South Sudan." www.oxfam.org). By combining conflict data with climate data, we aim to identify pivotal moments in conflict dynamics leading to unanticipated food insecurity.

Zero Hunger Labs (ZHL), in collaboration with the World Food Program (WFP), focuses on assessing and addressing acute malnutrition. ZHL's mission is to optimize WFP's workflow to enable more precise responses to global food crises. By analyzing data from WFP and publicly available sources, as well as photos and videos, ZHL aims to identify malnourishment and address gaps in medical attention.

Our research focuses on the districts Koch and Rubkona due to their shared climate zone which allows us to observe the impact of high-conflict events on food insecurity in Rubkona, a frontline district, as compared to the non-affected district, Koch. This comparative analysis provides a unique perspective on the potential influence of conflict dynamics on food security, informing future civil war development projections and facilitating the implementation of safety precautions to mitigate risks associated with potential catastrophic events.

Goal: To offer actionable insights for Zero Hunger Labs (ZHL), guiding aid strategies for food insecurity in the context of civil war development, through the analysis of information sourced from news articles and available weather signals.

### Research Question: 
How does the volume of conflict-related news articles influence IPC scores in a frontline district like Rubkona, in contrast to a less-violent district such as Koch, situated in the same climate zone?

## Evaluation and Interpretation of Results

In our evaluation methods, Mean Squared Error (MSE) was chosen because it is sensitive to larger errors.
This mitigated the impact that large deviations in IPC score predictions may have on the results, as such
deviations lead to limited awareness of food insecurity severity in affected areas. Additionally, a Bayesian
one-sided tail-area test is employed to check the probability of the observed causal impact of the
intervention that occurs by random chance. Furthermore, to minimize bias in our analysis, we implemented
manual topic and location labeling of 459 articles. This approach not only minimized bias, but also identified,
removed and corrected the misclassifications from the BERT model as well as filtered out articles not related
to Bentiu or Koch. Overall, this enhanced the accuracy and reliability of our research and the evaluation
process.

In interpreting our results, the Bayesian Structural Time series Model indicated a lasting impact of
significant conflict events on food insecurity. By clarifying a causal effect resulting from the Bentiu
takeover in particular, this model offered insightful information on the long-term effects of conflict events on
IPC scores. This understanding will be helpful in predicting the consequences of such large events in the
future. Moreover, regarding the prediction models for Koch and Rubkona, our research shows that using
four years of training data to establish a robust prediction model results in the lowest MSE scores. For
this project, the longer training period was important to achieve a high accuracy in predicting IPC scores for
these specific regions.

Our analysis revealed that there was a considerable decrease in the accuracy of IPC score predictions
during and following major conflict events. This underlined the difficulty in preserving a high quality and
reliability of food insecurity predictions in the face of major conflict events. One would have to to run the time
series intervention causal inference for a specific event to know if retraining of the OLS model is required.
One limitation of our analysis is that in other districts, more confounding variables could have a significant
impact on the IPC scores. Another limitation is that different districts get varying news coverage, as our
analysis focuses on the number of conflict related reports this would hinder the accurate predictions of IPC
scores from our model.

The project's reflection reveals that the model's effectiveness in predicting IPC scores is specific to Koch
and Rubkona due to variations in parameter weights among counties. Notably, the model accurately
forecasts the imminent impact of major events, enabling improved resource allocation. Future research
suggestions include refining the model by differentiating between types of conflicts through the incorporation
of dummy variables which requires an experts opinion.

With our analysis we are now able to answer our research question. We are able to model IPC scores
in Koch and Rubkona (two frontline districts of the civil conflict) effectively with the volume of conflict related
news articles and climate variables (see correlation and model section). Furthermore we found that a large
conflict event requires retraining the model due to the lasting impact.

Recommendations for Zero Hunger Labs (ZHL) involve cautioning against events with high violence
levels, suggesting retraining of prediction models based on the four most recent years. ZHL should extend
the model's application to more districts and cities, including the capital, Juba, for a broader understanding
of resource allocation needs. Although we were able to model IPC scores effectively for Koch and Rubkona
with just climate data and the number of conflict articles, for other districts ZHL should explore additional
confounding variables for model robustness as different geographical variables could be impacting the food
insecurity. Our third recommendation to ZHL is to make clear differentiations between civil war conflicts and
other conflicts to better be able to model the impact that civil war conflict has on forefront districts as it will
allow for improved recommendations for the shifting conflict dynamics.

This comparative analysis provided a unique perspective on the potential influence of conflict dynamics on
food security, informing future civil war development projections and facilitating the implementation of safety
precautions to mitigate risks associated with potential catastrophic events.

## Code description

### Hand-labeling
_1.articles_from_district.ipynb is the first notebook. This notebook takes all the articles from _articles_summary_cleaned.csv_ and assigns the closest county to it. furthermore it filters the articles to only include Rubkona, Koch, and Gorgial East Articles. This becomes _articles_summary_cleaned_with_location.csv_

_2.topic_modelling.ipynb_, A BERTopic model is fit on _articles_summary_cleaned_with_location.csv_ then four categories/keywords (hunger, refugees, humanitarian, and conflict) are defined. These categories are used for categorising articles (or none if the article doesn’t match any of the categories). The conflict category will be used to filter down the number of articles that we as a group handlabeled

Next _3.named_entity_recognition.ipynb_ was used for handlabelling data. The first section of the notebook uses spacy which allowed us to pick up on key words and locations while manually labeling the articles from _articles_summary_cleaned_with_location.csv_.

The results of our handlabelling is in _article_handlabeled_v2_raw.csv_.Running the rest of the _3.named_entity_recognition.ipynb_ notebook will clean the handlabeled data and preprocess it for the input for the linear regression _merged_df_for_causality_v2.csv_

### Confounding Variables
_4.climate_investigation.ipynb_ looks into the cross correlations between climate variables and IPC scores. Provides insight into climate variables.

_5.BERTopic_2014_spikes.ipynb_ attempts to find additional confounding variables mentioned in the articles. No additional confounding variables found beesides violence.


### OLS, and Causal Analysis
_6.Final_OLS_models.ipynb_ creates 4 OLS models based on Granger Causality to explain how conflict events have lasting effect and hence a new model must be trained after such an event MSE scores used as metric.

_7.TS_Causal_impact_final.ipynb_ notebook implements Bayesian Structural Time Series Model from Google to see if an event had a causal impact. In our case if the Bentiu takeover had a causal impact on the ipc scores while controlling for the confounding variable of Climate


## Requirements
To install the requirements open Terminal (macOS)/Command Prompt (Windows) and run pip install -r requirements.txt. If you create a new environment in PyCharm, an icon should appear to install requirements. The code runs with Python 3.9.16.

Required libraries:
- bertopic==0.15.0
- pandas==1.4.4
- geopandas==0.13.2
- matplotlib==3.7.2
- statsmodels==0.14.0
- pycausalimpact==0.1.1
- seaborn==0.13.2
- scikit-learn==1.5.1
- spacy==3.7.0

For Spacy:
pip install -U pip setuptools wheel
pip install -U spacy
python -m spacy download en_core_web_sm

## Troubleshooting

If you encounter any issues while running the notebooks, try the following:
- check that you have all the necessary libraries installed and the correct versions of them
- check your Python version. In principle, the code should work with any Python versions higher than 3.9.16. If this is not the case, create a virtual environment that uses Python 3.9.16.
- check that the models folder exists (for placeholder _blank_ was placed in the folder)
- delete all contents in models folder
- issues with installing spacy go to: https://spacy.io/usage
