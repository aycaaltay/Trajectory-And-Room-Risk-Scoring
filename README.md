# Trajectory-And-Room-Risk-Scoring
Trajectory and Room Risk Scoring Structures for the Paint Fever Game

It uses Map 7 data and play throughs for two tasks:
1. Extracting abnormal trajectory to distinguish between the attacker human player and the simulated pedestrian
2. Running a risk score for every room that determines the risk for every room

## Getting Started

Use the requirements.txt to install all modules necessary.

## main.py 

**Parameters**:

_analysis_type:_ Assign the analysis number you want to do (takes integer values: 1 or 2)
1. To calculate room risk scoring
2. To calculate separating human player and pedestrians

_gameList_: The list of games to be analyzed (Should be introduced from a csv file or entered manually)
- The games should be played on Map 7. 

_method_preference_: The method preference for room scoring calculation. 
- ML: Machine Learning, specifically Convolutional Neural Networks

_no_pedestrians_: The number of pedestrians to be used in the simulation
- _no_pedestrians_ number of pedestrians are generated of each type (a total of 5*_no_pedestrians_) on Map 7 and then projected onto each game.
- Pedestrians are not simulated separately for each game. Same _no_pedestrians_ pedestrians are used on the games.
- There is no need to run the pedestrian simulation at every run unless the gameList is not changed.
- If gameList is updated, then simulations must be run.
