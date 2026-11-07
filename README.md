# OpenShift Application Deployment and Autoscaling

## Project Overview

This project demonstrates hands-on experience with **Red Hat OpenShift**, a Kubernetes-based container application platform.

I deployed a Node.js sample application using the OpenShift Developer Console, explored the application build and deployment process, configured container resource requests and limits, and implemented Horizontal Pod Autoscaling (HPA) based on CPU utilization.

The project was completed using the IBM Skills Network / Cognitive Class OpenShift lab environment.

## Technologies and Tools

- Red Hat OpenShift
- Kubernetes
- OpenShift CLI (`oc`)
- YAML
- Node.js
- Git and GitHub
- Horizontal Pod Autoscaler (HPA)

## Architecture and OpenShift Resources

The application uses the following OpenShift resources:

| Resource | Purpose |
|---|---|
| BuildConfig | Defines how the application is built |
| Build | Executes the application build |
| Deployment | Manages application replicas |
| Pod | Runs the application container |
| Service | Provides stable internal network access |
| Route | Exposes the application externally |
| Horizontal Pod Autoscaler | Automatically adjusts the number of replicas |

## Implementation

### 1. Application Deployment

- Imported a Node.js sample application from GitHub.
- Used the OpenShift Developer Console to create the application.
- Selected the Node.js builder image.
- Observed the application build and deployment process.
- Explored the resources automatically created by OpenShift.

### 2. Container Resource Management

Configured CPU and memory requests and limits for the application container.

```yaml
resources:
  limits:
    cpu: 30m
    memory: 100Mi
  requests:
    cpu: 3m
    memory: 40Mi
```

**Understanding the configuration:**

- CPU request: 3 millicores.
- CPU limit: 30 millicores.
- Memory request: 40 MiB.
- Memory limit: 100 MiB.

Resource requests specify the resources Kubernetes uses when scheduling containers, while limits define their resource usage boundaries.

### 3. Horizontal Pod Autoscaling

Created a Horizontal Pod Autoscaler using the Kubernetes `autoscaling/v2` API.

The HPA configuration:

| Setting | Value |
|---|---|
| Target Deployment | `nodejs-ex-git` |
| Minimum replicas | 1 |
| Maximum replicas | 3 |
| Resource metric | CPU |
| Target average utilization | 10% |

The HPA monitors CPU utilization and adjusts the number of Deployment replicas to maintain the configured target, within the minimum and maximum replica limits.

See [`kubernetes/horizontal-pod-autoscaler.yaml`](kubernetes/horizontal-pod-autoscaler.yaml).

### 4. Traffic Generation and Monitoring

Generated HTTP requests against the application to create load and explore autoscaling behaviour.

Example command:

```bash
for i in $(seq 1000); do
  curl -s -L "YOUR_OPENSHIFT_ROUTE_URL" &
done
```

Monitored the HPA and Pods using the OpenShift CLI:

```bash
oc get hpa -w
oc get pods -w
oc describe hpa nodejs-ex-git-hpa
```

### 5. OpenShift CLI Commands

Some of the commands used during the exercise:

```bash
# Check current OpenShift project
oc project

# List application resources
oc get all

# List Deployments
oc get deployments

# List Pods
oc get pods

# List Services
oc get services

# List Routes
oc get routes

# Check Horizontal Pod Autoscaler
oc get hpa

# Inspect HPA configuration
oc describe hpa nodejs-ex-git-hpa
```

## Repository Structure

```text
openshift-nodejs-deployment-autoscaling/
│
├── README.md
│
├── kubernetes/
│   ├── horizontal-pod-autoscaler.yaml
│   └── deployment-resources.yaml
│
├── commands/
│   └── openshift-commands.md
│
└── screenshots/
    ├── openshift-topology.png
    ├── build-complete.png
    ├── application-route.png
    └── hpa-autoscaling.png
```

## Key Learning Outcomes

Through this hands-on exercise, I gained practical experience with:

- Deploying containerized applications on Red Hat OpenShift.
- Understanding OpenShift build and deployment workflows.
- Working with Kubernetes Deployments, Pods and Services.
- Exposing applications externally using OpenShift Routes.
- Configuring CPU and memory resource requests and limits.
- Creating Horizontal Pod Autoscalers using YAML.
- Monitoring application resources using the OpenShift CLI.
- Understanding automatic scaling in Kubernetes-based environments.

## Practical Experience

This project represents practical lab work completed using IBM Skills Network / Cognitive Class.

It demonstrates my understanding of the application deployment lifecycle and basic workload management on OpenShift.

**Note:** Screenshots and autoscaling results should reflect the actual behaviour observed during the lab. The HPA configuration alone does not prove that automatic scaling was successfully triggered.
