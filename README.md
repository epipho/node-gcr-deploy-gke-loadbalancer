![AyeAye](https://github.com/shippableSamples/node-build-push-docker-hub/blob/master/public/resources/images/captain.png)

# Docker Build, Continuous Integration, and Deployment to Kubernetes using Kubectl CLI for a Node JS application
[![Run Status](https://api.shippable.com/projects/5885ecca11c45a1000af5760/badge?branch=master)](https://app.shippable.com/projects/5885ecca11c45a1000af5760)
[![Coverage Badge](https://api.shippable.com/projects/5885ecca11c45a1000af5760/coverageBadge?branch=master)](https://app.shippable.com/projects/5885ecca11c45a1000af5760)


A simple Node JS application with unit tests and coverage reports using mocha
and istanbul.   

This repo demonstrates the following features:
* Set up serverless CI, i.e. on Shippable-provided infrastructure
* Set up CD pipelines for a Google Container Engine (GKE) cluster
* Perform CI tests
* Perform docker build and push image to Google Container Registry (GCR)
* Automatically deploy image to TEST environment 
* Manually deploy image to PROD environment 
* Automatically provision GKE load balancers for each environment  

## Run CI for this repo on Shippable
* Fork this repo into your source code account (e.g. GitHub)
* Create an account (or login) on [Shippable](www.shippable.com) with your SCM account
* Create a [GCR integration](http://docs.shippable.com/integrations/imageRegistries/gcr/) on Shippable for your Google account
* Update the CI configuration in `shippable.yml` file with your integration names (see comments in file)
* Follow these [setup instructions](http://docs.shippable.com/ci/runFirstBuild/) to enable your forked repo for CI and run a build 

## Add Continuous Delivery pipelines to deploy to Kubernetes

* Create an integration for [GKE](http://docs.shippable.com/integrations/containerServices/gke/)
* All pipeline config is in `shippable.resources.yml` and `shippable.jobs.yml`. Check these files and update config wherever the comment asks you to replace with your specific values
* Follow instructions to add your [Continuous Deployment pipeline](http://docs.shippable.com/tutorials/pipelines/howToAddSyncRepos/)
* Right-click on the deploy job in the SPOG view named 'shipdemo-deploy-gke-test' and run the job
  * This demo uses a declarative job type called 'deploy' in Shippable - [learn how moe about 'deploy' jobs](http://docs.shippable.com/pipelines/jobs/deploy/) 
* Your app should be deployed to your GKE cluster labeled as your TEST environment
* Follow instructions to [connect your Continuous Integration project to your Continuous Delivery pipelines](http://docs.shippable.com/tutorials/pipelines/connectingCiPipelines/)(for this demo, just uncomment the `trigger` integration in shippable.yml)
* Right-click on the deploy job in the SPOG view named 'shipdemo-deploy-gke-prod' and run the job to deploy as your PROD environment
* Make a change to your forked repo and commit to GitHub - watch your pipeline automatically execute CI with push to GCR and automatic deployment to the TEST environment in GKE
* Then right-click to deploy the newest changes to the PROD environment

Your end-to-end pipeline is complete! Now, any change you make to the application will be deployed to your GKE TEST environment and be ready to manually deploy to your PROD environment, as well.

### CI console screenshot
![CI Console Log](https://github.com/shippableSamples/node-gcr-deploy-gke-loadbalancer/blob/master/public/resources/images/shipdemo-gke-loadbalancer-CI.png)

### GCR integration screenshot
![Integration View](https://github.com/shippableSamples/node-gcr-deploy-gke-loadbalancer/blob/master/public/resources/images/shipdemo-gke-loadbalancer-GCR.png)

### CD pipeline  screenshot
![CD Pipeline](https://github.com/shippableSamples/node-gcr-deploy-gke-loadbalancer/blob/master/public/resources/images/shipdemo-gke-loadbalancer-CD.png)
