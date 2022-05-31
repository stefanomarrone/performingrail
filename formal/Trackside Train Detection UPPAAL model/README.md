# Trackside Train Detection Management UPPAAL model
This is the timed automata model described in the PerformingRail Deliverable D2.2, dedicated to the description of the function: Trackside Train Detection Management.
To set up our models, some peripheric automata have also been added to emulate the interactions of the aforementioned function with the other functions involved in the MB system (Train position reporting, Track Status Management, Trains Management), as well as with some external actors (TTD, TMS)

## Prerequisites
<<tools to install>>

In order to visualize and manipulate the model, UPPAAL tool has to be installed on your machine from the official website: https://uppaal.org/downloads/. Please follow Installation Instructions. 
Once the model has been added to the UPPAAL directory it can be edited and used for simulation and verification purposes.

## Usage

An UPPAAL model is constituted of various timed automata templates (possibly parameterizable) that can be instantiated to establish the model of the actual system to be investigated.
 Concretely, this latter is a network of timed automata that correspond to the composition of the instances created from these templates. 

Our model contains 8 templates:

- ``TTD" automaton which emulates the status change of the TTD block. This automaton sends the TTD status every desynchronization timeout.
	This automaton has as parameters ID_TDD, the ID of the TTD and initStatus, the initial status of TTD.

- ``TTDM_ReceiveTTD" automaton which represents a part of the behaviour of the ``TTD_Management" function. It receives the report from TTD automaton. 
	In the case that a desynchronization timer is assigned to a TTD (due to status inconsistency issue) and
	if in the next status reporting the status of the TTD is still reported as clear, the TMS is alerted about this abnormal situation. 
	This automaton has as parameters ID_TDD, the ID of the TTD.
	
- ``TM_SendTrainInfo" automaton which emulates the behaviour of the ``Trains_Management" function. 
	It sends Train information to the automaton ``TTDM_ReceiveTrainInfo" upon receiving a train position report.
	This automaton has as parameter ID_Train, the ID of the train.

- ``TTDM_ReceiveTrainInfo" automaton which represents a part of the behaviour of the ``TTD_Management" function. 
	It receives the train information from ``TM_SendTrainInfo" automaton. 
    This automaton has as parameter ID_Train, the ID of the train.
	 
- ``TTDManagement" automaton which represents a part of the behaviour of the ``TTD_Management" function. 
	It performs a synchronization between the received train information and TTD report every synchronization timer using the function 'Synchronise()'.
	This function computes for each train, within the area of control of the ``TTD_Management", the MaxSFE, the minSFE, the MaxSRE and the minSRE. 
	
	In the case when the MaxSFE and the minSFE are located in a clear TTD, a desynchronization timer is triggered to this TTD,  
	to monitor whether the TTD is designated as occupied in the next TTD report. If it is not the case, the TMS is alerted. 
	
	In the case that the MaxSFE is located in a clear TTD and the minSFE is located in an occupied TTD then a ``shortening" must be performed ('checkShorten = true'). 
	
	In the case when the MaxSFE is located in an occupied TTD and the minSFE is located in a clear TTD, then the TMS shall be alerted. 
	 
- ``TMS_TTDM'' automaton emulating the behaviour of TMS which is alerted 
	either in the case that a TTD is clear while it should be occupied '(AlertTMS_Faulty_TTD [ID_TTD])', 
	or when the train location is incoherent with TTD occupancy ('AlertTMS_TTDM').
	This automaton has as parameters ID_TDD, the ID of the TTD.

- ``TrackStatus_TTD'' automaton which emulates the behaviour of the ``Track_Status_Management" function. 
	It receives from ``TTDManagement" automaton a release request, and sends a release completed.
  
- ``TPRManagement" automaton which represents a part of the behaviour of the ``TPR_Management" function. 
	It sends each T_CYCLOC a TPR to `TM_SendTrainInfo" automaton.
	This automaton has as parameter ID_Train, the ID of the train.

In the system composition, we instantiate each required template with the relevant parameters, if any.
In our case, we consider a system composed of 10 TTD and 3 trains. 

## License
The software is licensed according to the GNU General Public License v3.0 (see License file).

## Feedback
Anyone can report bugs & suggestions on GitHub! Here's how it works:
* Click “New issue” and choose the appropriate format.
* Fill out the template with all the relevant info.
