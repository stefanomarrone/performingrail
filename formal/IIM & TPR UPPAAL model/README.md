# Integrity Information Management and Train position reporting UPPAAL model
This is the Timed Automata model described in the PerformingRail Deliverable D2.2, dedicated to the description of the functions:  Integrity Information Management and Train position reporting. 
To set up our models, some peripheric automata have also been added to emulate the interactions of the two
aforementioned functions with the other functions involved in the MB system (Speed and Distance Supervision, Trains Management), as well as with some external actors (Driver, TIMS, TLU).


## Prerequisites
In order to visualize and manipulate the model, UPPAAL tool has to be installed on your machine from the official website: https://uppaal.org/downloads/. Please follow Installation Instructions. 
Once the model has been added to the UPPAAL directory it can be edited and used for simulation and verification purposes.

## Usage
An UPPAAL model is constituted of various timed automata templates (possibly parameterizable) that can be instantiated to establish the model of the actual system to be investigated.
 Concretely, this latter is a network of timed automata that correspond to the composition of the instances created from these templates. 

Our model contains 11 templates:

- ``TIMS" automaton which emulates the behaviour of the TIMS block by sending 3 signals:  'Train_Integrity_Unknown', 'Train_integrity_Confirmed' and 'Train_Integrity_Lost'.
	It has as parameter ID_Train, the ID of the train.

- ``Driver" automaton which emulates the behaviour of the Driver block by sending signal 'Integrity_Confirmed_By_Driver".
	It has as parameter ID_Train, the ID of the train.

- ``Train mode" automaton which emulates the switching between the different ETCS operation modes. It is designed particularly in order to consider condition 8 (see PerformingRail Deliverable D2.2).
	It has as parameter ID_Train, the ID of the train.
	All the switching conditions are summarized in Table 8.1 of PerformingRail D2.2.

 
- ``Train localization Unit" automaton, which emulates the behaviour of the Train localization Unit. It regularly receives from the ``train position reporting" automaton requests for location. 
    It computes the location and sends it back to the ``Train position reporting" automaton.
 
- ``Train speed" automaton which emulates the speed of the train by sending the train speed information to the automaton ``Speed and Distance supervision". 
	Two values of speed are considered: 0 (Train is at standstill) and 1 (Train is moving). This automaton is designed particularly in order to consider condition 2 in the switching table. 
    
- `Train data" automaton which sends to the function ``Speed_and_Distance_Supervision" signals 
	'VALID_TRAIN_DATA' and 'INVALID_TRAIN_DATA'. Train data are required to compute integrity status (conditions 1, 2, 3, 4).
 
- ``Speed and Distance supervision" automaton receives from ``Train Data" automaton the signals about Train data,
	sends these information to the Trains_Management and waits for acknowledgement from this latter.
	This automaton also receives the train speed information from ``Train speed" automaton and can, therefore, determine whether the train is in standstill or not.
 
- ``IIM_StatusManagement" automaton which intercepts TIMS and Driver signals, 
	and, according to the current integrity status and other switching conditions (cf. Table 8.1 of D2.2), 
	performs the switching from one state to another.
      
- ``IIM updating" automaton which sends every INTEGRITY_CHECK_TIMEOUT the current integrity status to the ``Train_Position_Reporting" automaton.
	  
- ``Train_Position_Reporting" automaton which receives the current integrity status from ``IIM updating" automaton and sends the train position report to ``Trains_management".
	
- ``Trains_management" automaton which receives Train position report from The ``Train_Position_Reporting" automaton, and 
 receives Train Data from ``Speed and Distance supervision" automaton, and sends an acknowledgement upon reception. 
 
In the system composition, we instantiate each required template with the relevant parameters, if any.
 
We have also set a list of properties that can be checked by means of the UPPAAL Verfier engine. 
One should select in the Options of verification, diagnostic trace, shortest (for example). 
Select the property and press check. In the Simulator, you can view the trace.
One can also simulate the model by using the UPPAAL Simulator. In this case, the user can proceed step by step by choosing the transition
to fire if several ones are enabled. This is a particularly useful facility for debugging for instance. 
 
## License
The software is licensed according to the GNU General Public License v3.0 (see License file).

## Feedback
Anyone can report bugs & suggestions on GitHub! Here's how it works:
* Click “New issue” and choose the appropriate format.
* Fill out the template with all the relevant info.
