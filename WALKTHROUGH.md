# Logistics Wizard Walkthrough

For this walkthrough, you can use the shared deployment available at https://logistics-wizard.mybluemix.net/ or deploy your own version using [the toolchain](https://github.com/IBM-Cloud/logistics-wizard-toolchain).

You are going to play the role of a supply chain manager. You are working with a global retail company with multiple distribution centers, retail stores and a bunch of ongoing shipments.

1. Go to the home page of the web user interface, i.e https://logistics-wizard.mybluemix.net/ or the url of the *webui* app if you deployed your own.

  > The source code for the webui is available [here](https://github.com/IBM-Cloud/logistics-wizard-toolchain).

1. The homepage acts mainly as a portal to the app source and a starting point for this walkthrough.

1. Click on **View Logistics Wizard in action**.

  > If you were really working for this company you would have your own set of credentials to log into the application. Here we did not want you to have to think about any credentials. So instead we choose to automatically generate an isolated environment - with its own data set - when you click on this button. The environment will be the same every time you click the button. The benefit is that you can play with the deployment without being impacted by the actions of other users.

1. The dashboard shows up. It gives the supply chain manager an overview of ongoing shipments on a map.

  > The distribution centers, retail stores and shipments are retrieved from [the ERP simulator](https://github.com/IBM-Cloud/logistics-wizard-erp) by going through [the controller](https://github.com/IBM-Cloud/logistics-wizard-controller).

1. Select a distribution center. It shows outgoing shipments from this distribution center.

1. Select a retail store. It shows incoming shipments and the weather at this location.

  > The weather information is retrieved  by going through [the controller](https://github.com/IBM-Cloud/logistics-wizard-controller) which in turn calls an OpenWhisk action defined in [the recommendation service](https://github.com/IBM-Cloud/logistics-wizard-recommendation).

1. Select a shipment. It shows its current location and the current weather for this location.

1. Close the detail view.

1. You may have noticed the **Simulate Storm** button on the map. We don't control the weather but we can inject into the recommendation service a fabricated event to trigger the generation of new shipment recommendations.

1. Press **Simulate Storm**.

  > When you press the button, an OpenWhisk action is called in [the recommendation service](https://github.com/IBM-Cloud/logistics-wizard-recommendation) to generate suggested shipments given the storm event.

1. After a short while, an alert is displayed, the map is updated and shows the area impacted by the storm.

1. Select the storm area on the map.

1. The storm information panel is displayed. It shows the weather conditions and the suggested additional shipments.

1. As a supply chain manager, you can decide whether to approve or reject the suggested shipments.

1. Approve one shipment and reject the other.

  > Approve and reject are two other OpenWhisk actions in [the recommendation service](https://github.com/IBM-Cloud/logistics-wizard-recommendation).

1. Both recommendations disappear from the details.
