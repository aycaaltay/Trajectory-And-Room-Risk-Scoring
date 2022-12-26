# Trajectory-And-Room-Risk-Scoring
Trajectory and Room Risk Scoring Structures for the Paint Fever Game

It uses Map 7 data and play throughs for two tasks:
1. Extracting abnormal trajectory to distinguish between the attacker human player and the simulated pedestrian
2. Running a risk score for every room that determines the risk for every room

# main.py 

**Parameters**:

_analysis_type:_ Assign the analysis number you want to do (takes integer values: 1 or 2)
1. To calculate room risk scoring
2. To calculate separating human player and pedestrians

_gameList_: The list of games to be analyzed (Should be introduced from a csv file or entered manually)
- The games should be played on Map 7. 

