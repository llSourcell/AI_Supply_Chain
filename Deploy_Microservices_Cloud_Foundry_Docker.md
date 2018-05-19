# Instructions to Deploy Microservices as Cloud Foundry Docker Apps

These are instructions to deploy Logistic Wizard to Bluemix. The Webui, ERP, and Controller can be deployed to Bluemix Cloud Foundry. The ERP and Controller services will be pushed to Bluemix CF using docker images while the Webui will be deployed as a regular CF app.

## Set up the ERP

1. Set up the database for the ERP:
```
bx cf create-service bx cf create-service elephantsql turtle logistics-wizard-erp-db
```
2. Then clone `logistics-wizard-erp` repo:
```
git clone https://github.com/IBM-Cloud/logistics-wizard-erp
cd logistics-wizard-erp
```

3. Build and push the image to docker hub.
```
docker build -t <username>/logistics-wizard-erp:latest .
docker push <username>/logistics-wizard-erp:latest
```
4. Create the ERP microservice in bluemix without starting it using the docker image you created above
```
bx cf push <erp-name> --docker-image=<username>/logistics-wizard-erp:latest --no-start
bx cf bind-service <erp-name> logistics-wizard-erp-db
```
5. Start the ERP microservice
```
bx cf start <erp-name>
```
6. After starting the ERP microservice, you can verify it is running by hitting `https://<erp-name>.mybluemix.net/explorer`

## Set up the Controller Service

7. Clone the controller repo:
```
git clone https://github.com/IBM-Cloud/logistics-wizard-controller
cd logistics-wizard-controller
```
8. Build and push the image to docker hub.
```
docker build -t <username>/logistics-wizard-controller:latest .
docker push <username>/logistics-wizard-controller:latest
```
9. Create the controller microservice in bluemix without starting it using the docker image you created above
```
bx cf push <controller-name> --docker-image=<username>/logistics-wizard-controller:latest --no-start
```
10. Set the environment variables for the controller to connect to the ERP and use OpenWhisk actions
```
bx cf set-env <controller-name> ERP_SERVICE 'https://lw-erp-cf-docker.mybluemix.net/explorer'
bx cf set-env <controller-name> OPENWHISK_AUTH <openwhisk-auth>
bx cf set-env <controller-name> OPENWHISK_PACKAGE lwr
```
11. Start the controller microservice
```
bx cf start <controller-name>
```

## Set up the OpenWhisk Actions

1. Create the services needed for OpenWhisk
```
bx cf create-service weatherinsights Free-v2 logistics-wizard-weatherinsights
bx cf create-service cloudantNoSQLDB Lite logistics-wizard-recommendation-db
```

2. Create service keys for both services and take note of the URL values:
```
bx cf create-service-key logistics-wizard-weatherinsights for-openwhisk
bx cf create-service-key logistics-wizard-recommendation-db for-openwhisk
bx cf service-key logistics-wizard-weatherinsights for-openwhisk
bx cf service-key logistics-wizard-recommendation-db for-openwhisk
```

3. Clone the logistics-wizard-recommendation repo:
```
git clone https://github.com/IBM-Cloud/logistics-wizard-recommendation
cd logistics-wizard-recommendation
```
4. Copy the local env template file
```
cp template-local.env local.env
```
5. Using the URL values from above update the `local.env` file to look like the following:
```
PACKAGE_NAME=lwr
CONTROLLER_SERVICE=<controller-service-url>
WEATHER_SERVICE=<logistics-wizard-weatherinsights-url>
CLOUDANT_URL=<logistics-wizard-recommendation-db-url>
CLOUDANT_DATABASE=recommendations
```
6. Build your openwhisk actions:
```
npm install
npm run build
```
7. Deploy your OpenWhisk actions:
```
./deploy.sh --install
```

## Set up the WebUI

1. Clone the logistics-wizard-webui repo:
```
git clone https://github.com/IBM-Cloud/logistics-wizard-webui
cd logistics-wizard-webui
```
2. Install the dependencies
```
npm install
```
3. Build the static files for the UI using the appropriate environment variables
```
CONTROLLER_SERIVCE='<controller-service-url>' GOOGLE_MAPS_KEY='<google-maps-api-key>' npm run deploy:prod
```
4. Deploy the app to bluemix
```
cd dist
bx cf push <webui-name> -b staticfile_buildpack
```
