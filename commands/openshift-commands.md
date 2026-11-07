# OpenShift CLI Commands

## Check the current project
oc project

## List application resources
oc get all

## List Deployments
oc get deployments

## List Pods
oc get pods

## List Services
oc get services

## List Routes
oc get routes

## Check the Horizontal Pod Autoscaler
oc get hpa

## Monitor autoscaling
oc get hpa -w

## Monitor Pod creation
oc get pods -w

## Inspect HPA configuration and events
oc describe hpa nodejs-ex-git-hpa

## View Deployment configuration
oc describe deployment nodejs-ex-git

## Apply the HPA manifest
oc apply -f kubernetes/horizontal-pod-autoscaler.yaml