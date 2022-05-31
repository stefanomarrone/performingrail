## Points Management UPPAAL model
Points Management is the function of the trackside devoted to the management of points locking and unlocking in the PERFORMINGRAIL Deliverable 2.2. We have modelled the Points Management funtion via a network of different UPPAAL timed automata. We have one main automata which communicates with the other timed automata. The CreateRoute automata models the creating of the route, the SetandLock automata models the situation where we detect the final position of the point, SweepableandOverride timed automaton models the case of a sweeping train that frees some points.    

## Prerequisites
In order to manipulate the model, UPPAAL has to be installed on your machine from the official website: https://uppaal.org/downloads/. Please follow Installation Instructions. Once the model has been added to the UPPAAL directory it can be edited and used for simulation and verification purposes.

## Usage

The model consists of .... templates.



## License
The software is licensed according to the GNU General Public License v3.0 (see License file).

## Feedback
Anyone can report bugs & suggestions on GitHub! Here's how it works:
* Click “New issue” and choose the appropriate format.
* Fill out the template with all the relevant info.
