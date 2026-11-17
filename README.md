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

## Methodology

### Data and State Construction

The analysis uses play-by-play data from 199 matches of the 2021 AFL season, sourced from the publicly available dataset compiled by Richard Little. Each record contains time-stamped match events, including the event type, team and quarter.

A 15-state representation of match progression was constructed by combining the team in possession (home, away or neutral) with the inferred location of the ball. The location component distinguishes between the teams' attacking 50-metre zones, midfield, and scoring-related states such as goals, behinds and kick-ins.

Since the dataset does not contain precise player or ball tracking coordinates, field position is inferred from selected play-by-play events. Consequently, the spatial representation is relatively coarse, particularly in the midfield.

#### AFL Field Partition

[AFL Field Partition](figures/afl_partition_diagram.png)

*Figure 1: Partition of the AFL field into location zones
used in the semi-Markov model.*

### Semi-Markov Model

Match progression is represented using a discrete-state semi-Markov model. The sequence of states is modelled through a transition matrix, with transition probabilities estimated from the observed state sequences.

Unlike a continuous-time Markov chain, the semi-Markov framework allows holding times to have distributions beyond the exponential family. This enables the model to account for differences in the time spent in different possession-location states.

The fitted model is examined through its transition structure, holding-time distributions, long-run behaviour, expected scoring rates and convergence towards its stationary distribution. Monte Carlo simulations are also used to investigate whether the model reproduces the broad scoring characteristics observed in the 2021 season.

#### State Transition Diagram

[State Transition Diagram](figures/Transition_Flowchart.png)

*Figure 2: Common transitions between location-possession
states.*

#### Holding Time Distributions

[Holding time distributions](figures/holding_time_distributions.pdf)

*Figure 3: Distributions of holding times across the states of the semi-Markov model, illustrating the variation in time spent in each possession-location state before transitioning to another state.*

# Bayesian Forecasting

The semi-Markov framework is extended to forecast final match scores using several approaches to incorporate information observed during an ongoing match:

Null model: Uses fixed historical transition probabilities as a baseline.

Dirichlet model: Updates transition probabilities using current-match observations through Bayesian conjugate updating.

Exponentially Weighted Moving Average (EWMA): Gives greater weight to more recent match observations when updating transition probabilities.

Quarter-by-quarter model: Allows transition probabilities to vary between quarters to account for systematic changes in match dynamics.

The forecasting approaches are compared using mean absolute error (MAE), prediction bias and the consistency of improvements over the historical baseline.

#### Richmond vs Carlton Null Model Forecast
[Forecast versus actual plots](figures/forecastvsactual_richcarl.pdf)

*Figure 4: Comparison of predicted and actual scores throughout the 2021 Round 1 Richmond versus Carlton match, illustrating how the model's forecasts evolve as additional match information becomes available.*

[Home win probability plot](figures/diffswinprob_richcarl.pdf)

*Figure 5: Evolution of the home team's win probability throughout the 2021 Round 1 Richmond versus Carlton match, estimated through repeated simulations of the remaining match.*

## Key Results

### Semi-Markov Model

The fitted model captures meaningful structure in AFL possession and location dynamics. Its transition matrix exhibits an approximately banded structure, with transitions between neighbouring possession-location states dominating the process.

The model broadly reproduces the average scoring levels observed during the 2021 season. Simulated matches produce average scores of approximately 79.0 points for the home team and 74.5 points for the away team, compared with observed seasonal averages of approximately 79.8 and 75.4 points, respectively.

The model also exhibits relatively rapid convergence towards its stationary distribution, with a second-largest eigenvalue modulus of approximately 0.604. This supports the use of long-run quantities to investigate the proportion of transitions and time spent in different states.

### Forecasting Performance

The adaptive forecasting approaches produce modest improvements over the historical baseline. The EWMA model with a weighting parameter of β = 0.002 achieves the lowest overall mean absolute error of approximately 11.705 points, compared with 11.769 for the null model.

However, the improvements are relatively small and are not statistically significant after applying the Holm adjustment for multiple comparisons.

The quarter-by-quarter model does not achieve the lowest overall mean absolute error, but substantially reduces systematic prediction bias, particularly for away-team scores. This suggests that allowing scoring dynamics to vary throughout a match can provide benefits beyond simply increasing the weight assigned to recent observations.

Overall, the results highlight a trade-off between adapting to current-match information and retaining the stability of historical estimates.

#### Forecast Bias by Checkpoint

[Forecast bias plots](figures/forecast_bias_by_checkpoint.pdf)

*Figure 6: Comparison of forecast bias across quarter-time, half-time and three-quarter-time checkpoints, illustrating systematic differences between predicted and observed final scores.*

#### Forecast MAE by Checkpoint

[Forecast MAE plots](figures/forecast_mae_by_checkpoint.pdf)

*Figure 7: Mean absolute error of final-score forecasts across quarter-time, half-time and three-quarter-time checkpoints, comparing the predictive accuracy of the forecasting approaches.*

## Citation

If you use the code from this repository, please cite:

Faustin, Y. (2026). R Code for "Semi-Markov Models and Bayesian Methods in AFL". GitHub. https://github.com/yaronfaustin/Semi-Markov-Models-AFL

The underlying AFL play-by-play data should be attributed to:

Little, R. AFL Play by Play Data. GitHub. https://github.com/alittlefitness/afl_play_by_play
