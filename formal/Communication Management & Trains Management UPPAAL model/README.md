# Communication Management, Trains Management, Track Status Management UPPAAL model
This is the timed automata network described in the PerformingRail Deliverable 2.2, with Communication Management as the main automaton. It models the interaction between the CommunicationManagement function and the TrainsManagement and TrackStatusManagement functions regarding the Loss of Communication of a Train with the L3 Trackside system.

## Prerequisites
In order to manipulate the model, UPPAAL has to be installed on your machine from the official website: https://uppaal.org/downloads/. Once the model has been added to the UPPAAL directory it can be edited and used for simulation and verification purposes.

## Usage
In order for the system to work properly a process has to be instantiated for each train. In particular, the model contains six templates, three of which are detailed (CommunicationManager, TrainsManagement, TrackStatusManagement) and three of which are stubs (Train, RouteManagement, TrainIntegrity). The initialization template is, at the moment, not part of the model, but was added as it will be in the future.


## License
The software is licensed according to the GNU General Public License v3.0 (see License file).

## Feedback
Anyone can report bugs & suggestions on GitHub! Here's how it works:
* Click “New issue” and choose the appropriate format.
* Fill out the template with all the relevant info.
