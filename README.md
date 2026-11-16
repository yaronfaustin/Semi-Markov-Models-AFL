# Semi-Markov-Models-AFL
R code for the thesis: "Semi-Markov Models and Bayesian Methods in AFL"

## Abstract

This project applies semi-Markov models to Australian Rules Football (AFL), using play-by-play data from the 2021 season to represent match progression through location-possession states and state-dependent holding times.

The fitted model captures important features of AFL possession and scoring dynamics and broadly reproduces the observed average scoring rate. The framework is then extended to investigate final-score forecasting through several approaches, including Bayesian Dirichlet updating, exponentially weighted observations and quarter-by-quarter transition models.

The forecasting models demonstrate modest improvements over a historical baseline, with an exponentially weighted model achieving the lowest overall mean absolute error. Time-inhomogeneous models also help reduce systematic prediction bias. The study illustrates how semi-Markov and adaptive stochastic models can be used to analyse sporting dynamics and develop forecasts from sequential event data.


## Data

The AFL play-by-play data used in this project was obtained from the publicly available dataset compiled by Richard Little:

https://github.com/alittlefitness/afl_play_by_play

The data was originally sourced from afl.com.au and covers the 2021 AFL season.

## Citation

If you use the code from this repository, please cite:

Faustin, Y. (2026). R Code for "Semi-Markov Models and Bayesian Methods in AFL". GitHub. https://github.com/yaronfaustin/Semi-Markov-Models-AFL

The underlying AFL play-by-play data should be attributed to:

Little, R. AFL Play by Play Data. GitHub. https://github.com/alittlefitness/afl_play_by_play
