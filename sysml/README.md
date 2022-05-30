# SysML ETCS-L3 Specification

This folder contains the SysML model of ETCS-L3 according to the objective of the Performingrail project. The model is reported as a Papyrus model.

## Prerequisites

1.	If not on your PC, install Java SDK/JDK (https://www.oracle.com/fr/java/technologies/javase-downloads.html)
2.	As Papyrus runs under Eclipse IDE, install Eclipse IDE 2021-03 with Eclipse installer that can be downloaded on https://www.eclipse.org/downloads
3.	Launch the Installer and apply a filter to choose “Eclipse modeling tools”
4.	Launch Eclipse IDE 2021-03
5.	Go in Help > Eclipse Marketplace… and install Papyrus - SysML 1.6 (A simple link was on https://ci.eclipse.org/papyrus/job/papyrus-sysml16-master/ but a bug linked to the display of Model Explorer is corrected in the above mentioned update-site containing a nightly build of SysML compatible with current Eclipse version)

## Usage

The model is apportioned over different files to foster an easier distributed and collaborative environment. Each file is related to a different submodel/part of the whole model. This notwithstanding, the usage of the model is transparent to this division. Hence, there are in the folder many triplets of .di, .notation and .uml files.

To explore and contribute to the project, after cloning the repository in a local folder:
- (right click in the “Project Explorer”) > Import... > Git > Projects from Git > Next
- Choose the main branch of the repository and the location of your local workspace
- Open in the Project Explorer the file Perfomringrail
- Explore the model via “Model Explorer”


## License
The software is licensed according to the GNU General Public License v3.0 (see License file).

## Feedback
Anyone can report bugs & suggestions on GitHub! Here's how it works:
* Click “New issue” and choose the appropriate format.
* Fill out the template with all the relevant info.