# Mathematical background on weighting, summation and averaging

Multi-echo fMRI combination via weighted summation is a critical step in multi-echo post-processing that has been reported to increase temporal signal-to-noise ratio, decrease signal drop-out, and improve activation extent for task-analysis. The mathematics of all widely used multi-echo combination schemes are based on the underlying concepts of data weighting, summation and averaging. In this section we provide the basic mathematical equations to describe the underlying assumptions for echo combination schemes.

## Weighting, summation and averaging

Say we have a dataset $\{x_{1},x_{2},\dots ,x_{n}\}$ with elements $x_i$, and the dataset has corresponding weights $\{w_{1},w_{2},\dots ,w_{n}\}$ with elements $w_i$.\\
The notation for the dataset *summation} is*given by:

$
\sum_{i=i}^{n} x_{i}=x_{1}+x_{2}+\cdots+x_{n-1}+x_{n}
$

The *weighted summation* is calculated as the summation of the dataset after multiplying each element with its corresponding weight, thus:

$
\sum_{i=i}^{n} x_{i}w_{i}=x_{1}w_{1}+x_{2}w_{2}+\cdots+x_{n-1}w_{n-1}+x_{n}w_{n}
$

The *weighted average* or *mean* of the dataset is calculated by dividing the weighted summation by the sum of weights:

$
\bar{x}_{w}=\frac{\sum_{i=1}^{n} w_{i} x_{i}}{\sum_{i=1}^{n} w_{i}} = \frac{w_{1} x_{1}+w_{2} x_{2}+\cdots+w_{n} x_{n}}{w_{1}+w_{2}+\cdots+w_{n}}
$

A special case occurs when the weights are normalised (indicated by $w_{i}^{\prime}$) such that the sum of weights is equal to 1. Weights are normalised by dividing each weight element by the sum of weights, i.e.:

$
w_{i}^{\prime}=\frac{w_{i}}{\sum_{j=1}^{n} w_{j}}
$

And hence:

$
\sum_{i=1}^{n} w_{i}^{\prime}=1
$

Calculating the *weighted average* of the dataset using normalised weights}, we then get:
 
$
\bar{x}_{{w}^{\prime}}=\frac{\sum_{i=1}^{n} w_{i}^{\prime} x_{i}}{\sum_{i=1}^{n} w_{i}^{\prime}} =\sum_{i=1}^{n} w_{i}^{\prime} x_{i}
$

since the denominator, the sum of weights, is equal to 1.

It therefore follows that the *weighted average* of a dataset using ordinary non-normalised weights is equal to the *weighted summation* of the dataset when using *normalised weights*.


