# Soveren sample testing environment 

This chart deploys a Soveren testbed into your existing Kubernetes cluster, allowing you to evaluate Soveren's functionality hands-on without having to manage your own traffic.

## Installation

The primary pre-requisite is having the Soveren Agent deployed in one of your Kubernetes clusters. Refer to our [quick start guide](https://docs.soveren.io/en/stable/getting-started/quick-start/) for instructions on setting up the Agent.

For installing the Agent you will need the following:

- Soveren account. [Get one](https://app.soveren.io/sign-up) if you haven't already.
- A working [Helm](https://helm.sh) installation. Please refer to [documentation](https://helm.sh/docs) to get started.

## Installation

Add the Soveren testing Helm repository:

    helm repo add soveren-test https://soverenio.github.io/helm-charts-testing

If you had already added this repo earlier, run `helm repo update` to retrieve the latest versions of the packages.  You can then run `helm search repo soveren-test` to see the charts.

Install the `soveren-test` chart:

    helm install demo-load soveren-test/soveren-test

To uninstall the chart:

    helm delete demo-load

## How it works

Three containers with a minimal resource usage footprint are deployed into your Kubernetes cluster :

- `soveren-testing-sender`, henceforth referred to as `Sender`
- `soveren-testing-receiver`, henceforth referred to as `Receiver`
- `soveren-testing-satellite`, henceforth referred to as `Satellite`

Every 15 seconds, the `Sender` dispatches `HTTP` requests to the `Receiver`, `Satellite`, or the `Echo server` (the latter is situated in the Soveren Cloud).

These requests contain the following data:

```json
{
  "email": "john.doe@gmail.com",
  "seed": "!Www123456",
  "rememberMe": true,
  "timestamp": time.time()
}
```

For these requests, a collection of approximately 2000 random URLs is used, along with a single static URL that includes `Email`.

In response to these requests:

- The `Receiver` produces a `JSON` response composed of a random dataset that includes fields of type `Card`, `Email`, `Location`, `Person`, and `SSN`. This ensures that the derived dataset exhibits `high` sensitivity. For a comprehensive explanation, consult the [Sensitive data model](https://docs.soveren.io/en/stable/user-guide/data-model/#the-sensitivity-model).
- The `Satellite` generates a `JSON` response containing the `Email` field and several other random types, resulting in a `medium` sensitivity level.
- The `Echo server` simply echoes back whatever data it receives.

## What you should see in the Soveren app

As a result of deploying this chart, you will observe the following on the [data map](https://app.soveren.io/data-map):

![Data map with test assets](./img/data-map-overview.png "Data map with test assets")

There will be more pictures here