# Postman-Redfish-Collections

Postman collections for Redfish requests against HPE servers

This repository contains exported Postman collections in .json files as well as a typical environment with suitable variables holding everything needed to run Redfish requests smoothly.

The overall goal is to provide raw Redfish examples to understand the basic mechanic. Once this mechanic is digested you will be able to translate the examples into your favorite programing or scripting language (Python, PowerShell...).

It can help as well understand the examples posted in the [python-ilorest-library](https://github.com/HewlettPackard/python-ilorest-library/tree/master/examples/Redfish).

## Requirements

Install or upgrade to the latest version of [Postman](https://www.getpostman.com/apps) and make sure it is connected to the Internet.

## Import the Redfish generic environment

You need first to import the typical Redfish environment and customize it with your own values.

Download the [Redfish_generic.postman_environment.json](https://github.com/donzef/Postman-Redfish-Collections/blob/master/Redfish_generic.postman_environment.json) to your local computer. Start Postman and open the `Manage Environments` window (gear wheel icon in the upper right corner). Click on the import button, browse and select the just downloaded environment.  

Once this generic environment is imported, select it and customize the three variables according to your environment: `iloURI`, `iloUser` and `iloPasswd`. The `Token` and `SessionLocation` variables will be automatically populated during the iLO session creation. Hence you can leave them empty.

 Click on the `Update` button to save your changes.

You can now kill the `Manage Environments` popup window and select this new environment in the environment pull down list (upper right corner).

## Import collections

To use the various collections of this repository, you must import first the [1_Sessions](https://github.com/donzef/Postman-Redfish-Collections/blob/master/1_Sessions.postman_collection.json) collection. This collection contains iLO session management requests.

Copy in the clipboard the .json [collection URL](https://github.com/donzef/Postman-Redfish-Collections/blob/master/1_Sessions.postman_collection.json). Start Postman and click on `File` --> `Import...`. Select the `Import From Link` tabulation. Paste the URL in the dialog box and click `import`. You should see this new imported collection in the collection pane on the left side of Postman.

Use the same methodology to import other collections.

## Testing the environment

Expand the `1_Sessions` collection and click on the `Create iLO Session` request. Click on the `Send` button. If everything goes smoothly, you get a `201 Created` status code. You can verify that the `Token` and  `SessionLocation` variables have been populated by the `test` javascript. The `Token` variable will be to authenticate future requests. The `SessionLocation` will be used to delete the iLO session.

## Collection descriptions

### Redfish_generic

Generic Redfish Postman environment containing the remote iLO IP address as well as the remote iLO credentials required to open a session. It contains as well `Token` and `SessionLocation` variables required, respectively, to authenticate HTTP requests and delete the iLO session.

### 1_Sessions

Create, Delete and View iLO sessions. Use of the Postman `test` facility to capture the session Token and Session Location during the session creation.  

Read the [Managing iLO sessions with Redfish](https://developer.hpe.com/blog/managing-ilo-sessions-with-redfish) article to better understand iLO session management.

### 2_SmartStorage

Manage HPE Smart Array controllers. This collection has been created during the writing of the [Storage management with Redfish](https://developer.hpe.com/blog/storage-management-with-redfish) article.

### 3_VirtualMedia

This collection proposes mount and unmount Virtual drive requests using the Redfish standard and the legacy HPE Oem implementation. 

The first versions of the Redfish [VirtualMedia](http://redfish.dmtf.org/schemas/v1/VirtualMedia.json) were very limited in terms of actions and properties. However, in order to propose a decent user experience, HPE implemented its own Virtual Media subsystem under the Oem sub-tree, as permitted by the Redfish standard.

Today, and for backward compatibility, HPE implements both the Redfish VirtualMedia standard and its legacy Oem implementation.