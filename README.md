# Data Science Challenge: Earthquake prediction in Japan
##### Authors : Morisset Lucas, Danilo Fernandes, Frederico Testa, Omar Elkhalifi, Sébastion Vol

## Challenge Overview

Predicting earthquakes in Japan holds paramount importance due to the country's high susceptibility to seismic activities as part of the Pacific "Ring of Fire." The ability to forecast such natural disasters, even with limited precision or information, plays a critical role in ensuring public safety, protecting infrastructure, maintaining economic stability, ensuring nuclear safety, advancing scientific research, and building community resilience. Japan's frequent encounters with earthquakes necessitate preparedness and mitigation efforts that can significantly benefit from advancements in prediction capabilities. 

In this challenge, our objective is to leverage the self-exciting nature of earthquakes to attempt predictions regarding the timing and magnitude of future seismic events. The primary challenge lies in relying solely on historical earthquake data from Japan, without incorporating the country's geological characteristics into our predictive models.

## Data Description

Created by an act of Congress in 1879, the [USGS](https://www.usgs.gov/) provides science for a changing world, which reflects and responds to society’s continuously evolving needs. As the science arm of the US Department of the Interior, the USGS brings an array of earth, water, biological, and mapping data and expertise to bear in support of decision-making on environmental, resource, and public safety issues.

The dataset provided to participants was scrapped from the USGS' API, and can be found [here](https://earthquake.usgs.gov/fdsnws/event/1/). It contains all historical earthquake data in Japan between 2018 and 2023, and consists of :
- **Timestamps**: A column of timestamps indicating when earthquake occurred.
- **Magnitudes**: A column of magnitude associated with each earthquake.
- **Latitude**: Latitude of the epicenter.
- **Longitude**: Longitude of the epicenter.

Participants are expected to use this data only to train their models.

## Guidelines

The participants are expected to submit a generative model $G$ that generate timestamps and magnitudes data. Mathematicaly, from a random noises $(Z_i)_i \in \mathbb{R}^d_{latent}$, the participant must generate $(G(Z_i))_i = ((T_i,M_i))_i$. Note that the randomness can be an intrinsic part of the model's design (for exemple one can use a Poisson point process to generate the (T_i)_i sequence). 

## Evaluation Metric

Evaluation of models will be based on two key metrics:
- The **Anderson-Darling** metric between the generated magnitudes and the empirical magnitudes in the training dataset. This metric emphasizes differences in the distributions' extremes, placing greater emphasis on the tails that represent higher magnitudes and more destructive earthquakes.
- The **Wassertein distance** of the generated inter-arrival times and magnitudes vector $(v_i)_i = ((T_{i} - T_{i-1}, M_i, ..., T_{i+k-1} - T_{i+k-2}, M_{i+k-1}))_i$, in $\mathbb{R}^{2k}$ and its empirical counterpart. This measurement ensures the model captures both the self-exciting properties of earthquake occurrences and the correlations between earthquake magnitudes and frequencies.


Denote $\mu_{magnitude}$ the marginal distribution of the generated magnitudes, $\mu_{inter\_ arrival}$ the marginal distribution of the generated inter_arrival and magnitude vectors $(v_i)_i$, as well as $\hat{\mu_{magnitude}}$ and $\hat{\mu_{inter\_ arrival}}$ their empirical couterparts in the test dataset. Then the final metric used to rank the participants is :
$$ \mathfcal{L}(G) = AD(\mu_{magnitude}, \hat{\mu_{magnitude}}) + W_2(\mu_{inter\_ arrival}, \hat{\mu_{inter\_ arrival}})$$

The participants' goal should be to minimize $\mathcal{L}$.

For more details on any of these two metrics we refer to [Wikipedia:Anderson-Darling](https://en.wikipedia.org/wiki/Anderson%E2%80%93Darling_test) and [Wikipedia:W2](https://en.wikipedia.org/wiki/Wasserstein_metric)

## Baseline Model

As a starting point, we have provided a baseline Epidemic Type Aftershock Sequence (ETAS) model based on **Marked Hawkes Processes**. This model is a historical model used by geologists for earthquakes modelization and is further described in [Yosihiko Ogata & al.](https://link.springer.com/article/10.1023/A:1003403601725) The baseline model utilizes the temporal dependencies and the mark information in the data to make predictions. Participants are encouraged to explore beyond this baseline, incorporating innovative techniques and methodologies to improve upon the baseline performance.

We look forward to seeing your innovative solutions to this challenge. Good luck!