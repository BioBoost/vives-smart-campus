<!-- TODO: NEEDS UPDATE !!!!! -->

# Tasks of the Software Designers

The non limiting list of tasks of the software designers is:

* **Game Creator Engine**: software modules to create variants of \(city\) games. By means of a configuration file it should be possible to upgrade, modify or configure the embedded system firmware in the game box. The suggested format of the configuration file is a JSON \(JavaScript Object Notation\) based data-interchange format.
* **Visualization Software**: a Graphical User Interface \(GUI\) should be able to visualize the global status of the game, update the gameplay, summarize the status of the individual, competing teams, communicate with the individual teams, ... This software module acts as a kind of dispatching center for the game master.
* **History and Topscore Management System**:  a database should be maintained, interfaced, updated, secured. All database transactions should be handled by this software module. Scores for each game must be stored per named team. Results can be compared between different teams. A list of all games should be stored for future reference.
* **Media Web Server**: a Web Server should be able to collect and process media information, files, ... of the competing teams. Photos from a smartphone or tablet PC could be uploaded to the server. A File Management System or Content Management System could be valuable suggestions.
* **Game Management System**: this is the centralized, top level software framework, that seamlessly integrates all the above mentioned software modules. A programming language that supports Object Oriented Programming, multi-threading, ... is mandatory. The Game Management System should be able to interface with a database, visualize the status of the gameplay, process web content and media, interact with the game master, communicate with the competing teams, validate and process the results of the teams, ... 

The **Unified Modeling Language** \(UML\) methodology could be very useful to manage, design and maintain the global and partial parts of the software project \(an example is shown in the image below\). In a transparant and clear manner the structure \(attributes and behavior\) and relations between classes is visualized. This is a rather powerful tool for supporting the process of software development.

The following UML diagrams should be used to explain the development and results:

* Class diagram
* User stories
* Sequence diagrams
* Flowcharts
* State diagram

Note: Free educational accounts can be requested at [Lucidchart.com](https://www.lucidchart.com/). Just google for "lucid charts educational account".

![an example of UML software modelling](img/UML_class_diagram_hotel-949x683.png)

![Engineering quote](img/Engineering-quote-6.jpg)

