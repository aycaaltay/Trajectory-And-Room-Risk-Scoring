# Trajectory-And-Room-Risk-Scoring
Trajectory and Room Risk Scoring Structures for the Paint Fever Game

It uses Map 7 data and play throughs for two tasks:
1. Extracting abnormal trajectory to distinguish between the attacker human player and the simulated pedestrians
2. Running a risk score for every room that determines the risk for every room

## Getting Started

Use the requirements.txt to install all modules necessary. 
```
pip install -r requirements.txt
```

The rest can be run by the command
```
python main.py
```

Below, there are explanation of three main parts
1. The information on the main file (regardless of the task you want to do)
2. Information on methodology and outputs for calculating room scores
3. Information on methodology and outputs for distinguishing human player (attacker) and simulated pedestrians

## Main file information

### main.py 
You can select what you want to do and run the program.

**Parameters**:

**_analysis_type_**: Assign the analysis number you want to do (takes integer values: 1 or 2)
1. For calculating the room risk score, use 
```
analysis_type = 1
```
2. For distinguishing the human player and pedestrians, use
```
analysis_type = 2
```
No other values can be used at this stage. 

**_gameList_**: The list of games to be analyzed (Should be introduced from a csv file or entered manually)
- The games should be played on Map 7. 
- There are two ways to introduce the list of games to be analyzed.
1. Introducing through a .xlsx or .csv file
```
gameList = pd.read_excel("gameList.xlsx").values.tolist()
gameList = [item for sublist in gameList for item in sublist]
```
2. Entering manually
```
gameList = [48, 52, 132, 142, 153, 166, 222, 252, 343, 356, 390, 599, 779, 861, 862, 1044, 1058, 1067, 1182, 1268]
```
**_method_preference_**: The method preference for room scoring calculation. 
- ML: Machine Learning, specifically Convolutional Neural Networks
```
method_preference = "ML"
```

**_no_pedestrians_**: The number of pedestrians to be used in the simulation
```
no_pedestrians = 1000
```
- _no_pedestrians_ number of pedestrians are generated of each type (a total of 5*_no_pedestrians_) on Map 7 and then projected onto each game.
- Pedestrians are not simulated separately for each game. Same _no_pedestrians_ pedestrians are used on the games.
- There is no need to run the pedestrian simulation at every run unless the gameList is not changed.
- If gameList is updated, then simulations must be run.

**_second_indices_**: The partition of seconds for analysis. 
```
second_indices = [5]
```
- The above instance analyzes the first 5 seconds separately than the rest. 

## Calculating Room Risk Scores

### mainRoomScoring.py

Room scoring can be done with traditional statistical methods or with Convolutional Neural Networks. The data generation for either method is created in this file, and each related file will be presented separately. 

The initial task is to determine the output structure. The output can be binary or multiclass depending on the structure below. 
- If it's binary, the the room that the human player is in gets a value of 1, and the other rooms each get a value of 0.  **generateBinaryData.py** generates these outputs.
- If it's multi-class, the room that the human player is in gets a value of 0, and the other rooms get the adjacency value (number of hops) from that room as shown in the picture. **generateMulticlassData.py** generates these outputs.
- 
![alt text](https://github.com/aycaaltay/Trajectory-And-Room-Risk-Scoring/blob/main/Figures/Room%20Scoring.png =250x)

Similarly, both output types can be used for regression and classification. 
