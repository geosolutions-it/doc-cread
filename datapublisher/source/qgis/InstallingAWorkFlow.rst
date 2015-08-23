.. _installing-a-workflow:

########
Installing a workflow
########

After installing and activating the plugin, it also needs to be activated in Processing options which are accessible from QGIS main menu (Processing > Options and configuration). The path to the directory where the workflow files are stored (by default in the plugin directory) can also be set:

.. image:: img/QGIS_ProcessingOptions.png 


After the activation the workflow library can be accessed through the Processing Toolbox and also from an icon on the QGIS task bar:

.. image:: img/QGIS_WorkFlowLibrary.png

A workflow consists of a number of steps, with each step having an instruction pane on the left and the algorithm window on the right. After a step execution is started (by pressing the Run button) and completed, the next step will automatically open. It is also possible to skip steps without execution and go back to previous steps by using the buttons at the bottom of the workflow dialog:

.. image:: img/QGIS_workflow.png