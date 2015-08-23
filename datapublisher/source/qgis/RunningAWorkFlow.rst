.. _qgis_running_workflow:

##################
Running a workflow
##################

New workflows can be easily added by using the Workflow Creator which can be accessed from the Processing Toolbox
(Workflows > Tools > Create new workflow). 

Existing workflows can also be edited by right clicking on them and selecting Edit workflow:

.. image:: img/QGIS_WorkFlowEdit.png

In the Workflow Creator new algorithms can be added to a workflow by double clicking on any algorithm in the list
 on the left. 
 
 All algorithms available in the Processing Toolbox, including models and scripts, can be added to a workflow. 
 To remove an algorithm from a workflow the Remove step at the bottom of the dialog should be used. 
 
 The order of the algorithms can be changed by dragging the tabs with algorithm names at the top of the dialog. 
 To save a workflow its name and group should be entered at the top of the dialog and the save button clicked. 
 
 Workflows are saved in a text file which contains information on the number and order of steps, 
 the instructions for each step and any pre-set values of numeric, text, drop-down list or boolean algorithm parameters. 
 The workflows can also be tested before saving by using the Test button.

.. image:: img/QGIS_WorkFlowCreator.png
