# ACIC 2023 data competition

<details><summary>Table of Contents</summary><p>

* [Summary](#summary)
* [Why we made this competition](#why-we-made-this-competition)
* [Get the Data](#get-the-data)
* [Some details about the data](#some-details-about-the-data)
* [Estimand](#estimand)
* [Submission](#submission)
* [Dates](#dates)
* [Contact](#contact)
* [License](#license)
</p></details><p></p>

## Summary

In this repository you'll find data for the ACIC 2023 competition. This README
will provide all the information you need.

With this competition, we aim to search for the most appropriate methods for
forecasting counterfactuals. Traditional forecasting methods–built to minimise
observed error–are not built for counterfactuals. Traditional counterfactual
estimators–built for unbiased estimates of causal estimands–are not built for
forecasts. In this competition, we collectively can explore the trade off
between these methods and advance our understanding of both forecasting and
counterfactual estimation.

We welcome your participation and contributions to this exciting competition
and look forward to advancing the field together.  

In short:

- We want to understand the trade off between forecasting and counterfactual
  estimation
- Task is to make 30 predictions per unit: five steps, with outcomes under six
  different treatments. Loss is MSE over the units x 30 predictions.
- Data (simulated) found here, in this repository
- Competition runs March and April 2023. Results released at [ACIC
  2023](https://sci-info.org/annual-meeting/)
- Submissions [here](https://docs.google.com/forms/d/11RA7-n8MwBu4wSkoMXTkZ5XLvslOOHnvqnEXPCNgEjk/edit#settings)
- Enjoy :)

## Why we made this competition

This challenge helps address a critical challenge in industry.
Decision-makers – often algorithmic – rely on forecasts of outcomes under
different interventions to inform their choices.  For example, they want to
choose prices for items based on outcomes under different prices.

The current widely used approach is supervised learning, as seen in the M5
competition. A benefit of this approach is its scalability. However,
supervised learning falls short as it only fits observed outcomes to
predictions based on the observed intervention. The loss function does not
measure outcomes for interventions not taken.

Another approach uses observational causal inference techniques, as seen in
prior ACIC competitions. This method measures the difference in outcomes
between interventions but does not focus on the levels of future outcomes,
which are crucial for optimisation tasks.

Reinforcement learning offers a theoretical solution to this problem, but its
practical implementation is hindered by the large, complex state space and
legacy systems. Incremental improvements to legacy systems can provide a way
forward, but leaves us with the challenge of forecasting counterfactuals.

To address this challenge, participants in the ACIC23 competition will be
asked to forecast both observed and counterfactual outcomes. The competition
will provide a deeper understanding of the relationship between supervised
learning and counterfactual estimation and help improve decision-making
processes.

## Get the data

You'll find this above, `training_sample.csv`

## Some details about the data

The data consists of 3908 units, each with 95 time steps. There is an outcome
variable, a treatment variable consisting of six levels and six covariates. For
each unit, for each time step, we observe a single outcome and treatment. 

Some details about the data

- Non linear, dynamical system
- Conditional ignorability satisfied
- We don't have overlap 
- There are no spillovers across units, or direct spillovers over time
- Consistency is satisfied 
- Have to predict covariates

You have enough information to satisfy conditional ignorability. But due to
dynamics in the system, non linearities and the fact that it's a forecasting
task, we don't expect this to be enough.

There is not full overlap. This means that the probability of some treatment
levels given a context will be zero. This is by design, extrapolation is part
of the forecasting game. However, we do satsify SUTVA: one unit's treatment
only affects that treatment. Also, the treatment in a context has a single,
specific effect. A treatment at time $t$ only has a indirect affect on
outcomes at any time $j \neq t$.

Last, we don't provide predictions for covariates during the prediction
window. Of course, they would help you, but that's not what we're after :) 

Note: We've made effort to ensure that the data is free of bugs. This is a
simulated data of a dynamic system. Though you may still find bugs. If you
find a bug, please submit an issue in this repository or reach out
[here](https://forms.gle/EAgkSoqruZAS1WDT6). If we do find bugs, we will let
particpants know.

## Estimand

Our estimand is the root mean squared error over all forecast time steps and
counterfactual states. For each unit, there are five time steps and six
possible treatments. So there are thirty predictions per unit.

Where $N$ is the number of units, $N_K$ the number of time steps, $N_W$ the
number of treatments, $i$ a unit, $k$ a time step, $w$ a treatment, $y$ the
ground truth outcome and $\hat{y}$ the predicted outcome, the estimand is

```math 

    \sqrt{\frac{\sum_{i, k, w}(y_{i,k}(w) - \hat{y}_{i,k}(w))^2}{N * N_K * N_W }}

```

## Submission

Submissions have the following columns

  - 0.0      # outcome under treatment = 0.0
  - 0.1      # outcome under treatment = 0.1
  - 0.2      # outcome under treatment = 0.2
  - 0.3      # outcome under treatment = 0.3
  - 0.4      # outcome under treatment = 0.4
  - 0.5      # outcome under treatment = 0.5
  - unitID   # unit ID
  - step     # step number for prediction {1, 2, .., 5}

You can find an example in `predictions.csv`

Please submit your entry [here](https://forms.gle/sNi7d8wSUSB5zedW8)

## Dates

- March 1, 2023. Competition opens
- April 30, 2023. Competition closes
- May 24--26, 2023. Results released at [ACIC23](https://sci-info.org/annual-meeting/)

## Contact

Please use this [this
form](https://forms.gle/EAgkSoqruZAS1WDT6),
or open an issue in this repository.

## License

The MIT License (MIT) Copyright © [2023] Zalando SE, https://tech.zalando.com

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
