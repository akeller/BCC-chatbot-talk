# Watson Assistant (formerly Conversation) Sample Application for BCC Talk

This Node.js app demonstrates the Watson Assistant service in a simple chat interface simulating either a pizza ordering or wedding RSVP situation.

## Before you begin

* Create an IBM Cloud account
    * [Sign up](https://console.ng.bluemix.net/registration/?target=/catalog/%3fcategory=watson) in IBM Cloud, or use an existing account. Your account must have available space for at least 1 app and 1 service.
* Make sure that you have the following prerequisites installed:
    * The [Node.js](https://nodejs.org/#download) runtime, including the [npm][npm_link] package manager
    * The [Cloud Foundry][cloud_foundry] command-line client (not covered in this talk)

      Note: Ensure that your Cloud Foundry version is up to date

## Installing locally

If you want to modify the app or use it as a basis for building your own app, install it locally. You can then deploy your modified version of the app to IBM Cloud.

### Getting the files

Use GitHub to clone the repository locally.

### Setting up the Watson Assistant service

You can use an exisiting instance of the Watson Assistant service. Otherwise, follow these steps.

1. In your browser, navigate to [your IBM Cloud console] (https://console.ng.bluemix.net/dashboard/services).

1. Click the button to **Create Resource** and then filter using the side menu on "Watson". 

1. Click Watson Assistant and walk through the steps to start the service. A Lite account will be all that is necessary for this demo.

### Importing from Bot Asset Exchange (BAE) [optional]

1. In your browser, navigate to the [Bot Asset Exchange](https://developer.ibm.com/code/exchanges/bots/).

1. Choose a bot you want to use and click download.

1. Login with your IBM Cloud account information.

1. The page that loads contains your workspaces. Click the icon to import a workspace.

![alt text][workspaces]

1. Import the json file that you downloaded. Choose the file and import everything. This will create a new workspace with all the intents, entities, and dialog intact.

1. Click the new workspace tile to open it.

![alt text][Workspace-dashboard]

1. Click the Deploy icon.

1. Click Credentials (next to Deploy Options). Copy your workspace ID, username and password. Enter these as strings in the .env file to access the API.

![alt text][credentials]

...

Alternatively, from the IBM Cloud Conversation page (page where the Launch tool button sits), click "Service credentials" then expand "View credentials" to reveal your username and password. Enter these as strings in the .env file to access the API. This does not show your workspace ID.

### Importing the Watson Assistant workspace

1. In your browser, navigate to [your IBM Cloud console] (https://console.ng.bluemix.net/dashboard/services).

1. From the **All Items** tab, click the newly created Watson Assistant service in the **Services** list.

1. On the Service Details page, click **Launch tool**.

1. Click the **Import workspace** icon in the Watson Assistant service tool. Specify the location of the workspace JSON file in your local copy of the app project:

    [Watson Pizza Example](/watson_pizza.json)
    
    [Wedding RSVP Example](/weddingRSVP.json)

1. Select **Everything (Intents, Entities, and Dialog)** and then click **Import**. The workspace is created.

### Configuring the app environment

1. Copy or rename the `.env.example` file to `.env` (nothing before the dot).

1. Use the Assistant UI to get the username, password, and URL. 

1. Paste  the `password` and `username` values (without quotation marks) from the JSON into the `ASSISTANT_PASSWORD` and `ASSISTANT_USERNAME` variables in the `.env` file. For example:

    ```
    ASSISTANT_USERNAME=ca2905e6-7b5d-4408-9192-e4d54d83e604
    ASSISTANT_PASSWORD=87iT7aqpvU7l
    ```

1. In your IBM Cloud console, open the Watson Assistant service instance where you imported the workspace.

1. Click the menu icon in the upper-right corner of the workspace tile, and then select **View details**.

    ![Screen capture of workspace tile menu](readme_images/workspace_details.png)

1. Click the ![Copy](readme_images/copy_icon.png) icon to copy the workspace ID to the clipboard.

1. On the local system, paste the workspace ID into the WORKSPACE_ID variable in the `.env` file. Save and close the file.

### Installing and starting the app

1. Install the demo app package into the local Node.js runtime environment:

    ```bash
    npm install
    ```

1. Start the app:

    ```bash
    npm start
    ```

1. Point your browser to http://localhost:3000 to try out the app.

## Testing the app

After your app is installed and running, experiment with it to see how it responds.

The chat interface is on the left, and the JSON that the JavaScript code receives from the Watson Assistant service is on the right. 

For more information about intents, see the [Watson Assistant service documentation][doc_intents].

To see details of how these intents are defined, including sample input for each intent, launch the Watson Assistant tool.

## Modifying the app

After you have the app deployed and running, you can explore the source files and make changes. Try the following:

* Modify the .js files to change the app logic.
* Modify the .html file to change the appearance of the app page.
* Use the Watson Assistant tool to train the service for new intents, or to modify the dialog flow. For more information, see the [Watson Assistant service documentation][docs_landing].

## Deploying to IBM Cloud (not covered in this talk)

You can use Cloud Foundry to deploy your local version of the app to IBM Cloud.

1. In the project root directory, open the `manifest.yml` file:

  * In the `applications` section of the `manifest.yml` file, change the `name` value to a unique name for your version of the demo app.
  * In the `services` section, specify the name of the Watson Assistant service instance you created for the demo app. If you do not remember the service name, use the `cf services` command to list all services you have created.

  The following example shows a modified `manifest.yml` file:

  ```yml
  ---
  declared-services:
   my-watson-assistant-service:
     label: conversation
     plan: free
  applications:
  - name: conversation-simple-app-test1
   command: npm start
   path: .
   memory: 256M
   instances: 1
   services:
   - my-watson-assistant-service
   env:
     NPM_CONFIG_PRODUCTION: false
  ```

1. Push the app to IBM Cloud:

  ```bash
  cf push
  ```
  Access your app on IBM Cloud at the URL specified in the command output.

## Troubleshooting

If you encounter a problem, you can check the logs for more information. To see the logs, run the `cf logs` command:

```none
cf logs <application-name> --recent
```

## License

This sample code is licensed under Apache 2.0.
Full license text is available in [LICENSE](LICENSE).

## Contributing

See [CONTRIBUTING](CONTRIBUTING.md).

## Open Source @ IBM

Find more open source projects on the
[IBM Github Page](http://ibm.github.io/).


[cf_docs]: (https://console.bluemix.net/docs/services/watson/getting-started-cf.html)
[cloud_foundry]: https://github.com/cloudfoundry/cli#downloads
[demo_url]: http://conversation-simple.ng.bluemix.net/
[doc_intents]: (https://console.bluemix.net/docs/services/conversation/intents-entities.html#planning-your-entities)
[docs]: https://console.bluemix.net/docs/services/conversation/index.html
[docs_landing]: (https://console.bluemix.net/docs/services/conversation/index.html)
[node_link]: (http://nodejs.org/)
[npm_link]: (https://www.npmjs.com/)
[sign_up]: bluemix.net/registration
