# Powerfulseal Helm Chart

A Helm chart for [Powerfulseal](https://github.com/powerfulseal/powerfulseal), a tool that injects failures into Kubernetes clusters.

## Overview
This helm chart serves as a wrapper to orchestrate the deployment of Powerfulseal policies. The chart deploys the necessary Kubernetes resources into the given namespace, running the provided policies in autonomous mode.

## Prerequisites
- [Helm](https://helm.sh/docs/intro/quickstart/)
- [kubectl](https://kubernetes.io/docs/reference/kubectl/overview/) (with access to the target cluster)
- A [namespace](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/) for the Powerfulseal instance
- The Powerfulseal Helm chart

## Configuration
The Powerfulseal instance and its policies/scenarios can be configured in a [values file](https://helm.sh/docs/chart_template_guide/values_files/) as shown below:

```
# values.yaml

powerfulseal:
  image:
    repository: bloomberg/powerfulseal
    imagePullPolicy: Always
    tag: 3.0.1

  policies: |
    config:
      runStrategy:
        minSecondsBetweenRuns: 30
        maxSecondsBetweenRuns: 300
    scenarios: []

  args: []
```

### Policies
`powerfulseal.policies` contains a multi-line string that essentially contains the contents of a policy file used in a standard Powerfulseal deployment. More information on configuring and applying this can be found [here](https://powerfulseal.github.io/powerfulseal/policies). It may be easier to create a separate policy YAML file, and then paste the contents into the values file.

## Usage
Download the Helm chart to the same working repository as your configuration file and run the following:

`helm install {RELEASE-NAME} ./powerfulseal --namespace {POWERFULSEAL-NAMESPACE} -f {VALUES-FILE}`

## Removal

`helm uninstall {RELEASE-NAME} --namespace {POWERFULSEAL-NAMESPACE}`
