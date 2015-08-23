.. _installing-workflow-plugin:


########
Installing workflow plugin
########

Processing Workflows is a plugin for QGIS for creating processing workflows. The workflows provide step-by-step instructions and guidance for less experienced users thus facilitating capacity building in Earth observation data analysis and GIS tasks.

QGIS has been designed with a plugin architecture. This allows many new features and functions to be easily added to the application. 
You can manage your plugins in the plugin dialog which can be opened with **Plugins** > **Manage and install plugins**.

.. image:: img/QGIS_PlugIn.png

The menus in the Plugins dialog allow the user to install, uninstall and upgrade plugins in different ways. Each plugin have some metadatas displayed in the right panel:

- information if the plugin is experimental
- description
- rating vote(s) (you can vote for your prefered plugin!)
- tags
- some useful links as the home page, tracker and code repository
- author(s)
- version available

Here, all the available plugins are listed, including both core and external plugins. this menu lists all plugins available that are not installed. Choose Not Installed, in Search function type "Processing Workflows" select it in the list and click Install plugin button to implement it into QGIS.

.. image:: img/QGIS_GestionePlugIn.png

In Settings menu, you can use the following options:

- Check for updates on startup. Whenever a new plugin or a plugin update is available, QGIS will inform you ‘every time QGIS starts’, ‘once a day’, ‘every 3 days’, ‘every week’, ‘every 2 weeks’ or ‘every month’.
- Show also experimental plugins. QGIS will show you plugins in early stages of development, which are generally unsuitable for production use.
- Show also deprecated plugins. These plugins are deprecated and generally unsuitable for production use.

To add external author repositories, click [Add...] in the Plugin repositories section. If you do not want one or more of the added repositories, they can be disabled via the [Edit...] button, or completely removed with the [Delete] button.

.. image:: img/QGIS_SettingsPlugIn.png



