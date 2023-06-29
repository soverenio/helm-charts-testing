## Usage of testing data load generator

This chart installs a couple of containers generating real http traffic to your infra. 

[Helm](https://helm.sh) must be installed to use the charts.  Please refer to
Helm's [documentation](https://helm.sh/docs) to get started.

Once Helm has been set up correctly, add the repo as follows:

    helm repo add soveren-test https://soverenio.github.io/helm-charts-testing

If you had already added this repo earlier, run `helm repo update` to retrieve
the latest versions of the packages.  You can then run `helm search repo
soveren-test` to see the charts.

To install the `soveren-test` chart:

    helm install demo-load soveren-test/soveren-test

To uninstall the chart:

    helm delete demo-load
