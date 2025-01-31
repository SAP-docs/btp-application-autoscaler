<!-- loiof3e7fa907e9d4da89fc55602818bd6f4 -->

# Initial Setup

Create an instance of the Application Autoscaler service and bind it to your application. Install Autoscaler's plug-in for the “Cloud Foundry CLI” and attach a policy to your application.



<a name="loiof3e7fa907e9d4da89fc55602818bd6f4__prereq_cmh_s3x_5z"/>

## Prerequisites

> ### Note:
> If you are using this service as part of SAP Build Code, follow the [SAP Build Code Initial Setup](https://help.sap.com/docs/build_code/d0d8f5bfc3d640478854e6f4e7c7584a/07698d7c31284e4db370acdf017cfd14.html?version=SHIP) instructions instead.

-   You have downloaded and set up the Cloud Foundry Command Line Interface \(cf CLI\). See [Download and Install the Cloud Foundry Command Line Interface](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/4ef907afb1254e8286882a2bdef0edf4.html "Download and set up the Cloud Foundry Command Line Interface (cf CLI) to start working with the Cloud Foundry environment.") :arrow_upper_right:.
-   You are logged on to your Cloud Foundry space. See [Log On to the Cloud Foundry Environment Using the Cloud Foundry Command Line Interface](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/7a37d66c2e7d401db4980db0cd74aa6b.html "Use the Cloud Foundry Command Line Interface (cf CLI) to log on to the Cloud Foundry space.") :arrow_upper_right:.
-   You are a Space Developer in the chosen Cloud Foundry space.
-   You have deployed the application you want to scale in the Cloud Foundry environment. See [Deploy Business Applications in the Cloud Foundry Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/4946ea5421374924963ce8575a5f3d05.html "When an application for the Cloud Foundry environment resides in a folder on your local machine, you can deploy it and start it by executing the command line interface (CLI) command push. To deploy business applications bundled in a multitarget application archive, you have to use the command deploy-mta.") :arrow_upper_right:.



## Procedure
### Bind your application
1.  Check if the Application Autoscaler service is listed in the Service Marketplace using the following command:

    ```shell
    cf marketplace
    ```

2.  Create an instance of the service using the following command:

    ```shell
    cf create-service autoscaler <service plan name> <instance name>
    ```

    > ### Sample Code:
    > ```shell
    > cf create-service autoscaler standard myservice
    > ```

3.  Bind the service instance to your application using the following command. You can bind as many applications as you want to an Application Autoscaler service instance.

    ```shell
    cf bind-service <application name> <instance name> -c <file name>.json
    ```

    The JSON file contains the policy, which is needed to initiate the scaling of an application. For more information about how to define a policy, see [Defining a Scaling Policy](defining-a-scaling-policy-79f443a.md).

    > ### Note:
    > If you are building a multitarget application \(MTA\), you can leverage the MTA deployment descriptor to provide the scaling policy. See [Service Binding Parameters](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/c7b09b79d3bb4d348a720ba27fe9a2d5.html).

4.  Check if the instance is successfully bound to the application using the following command:

    ```shell
    cf service <instance name>
    ```

    The *Bound apps* field displays all applications bound to the instance.

### Install Autoscaler's plug-in for the “Cloud Foundry CLI”
The plug-in can easily be installed directly via the command-line:
```shell
cf install-plugin -r CF-Community app-autoscaler-plugin
```

For further installation-options, please look into the [documentation](<https://github.com/cloudfoundry/app-autoscaler-cli-plugin#install-plugin>) on its official repository on GitHub.

### Attach a policy
 1. Create a file named “app-policy.json” with the following content:
    ```json
    {
      "instance_min_count": 1,
      "instance_max_count": 2,
      "scaling_rules": [
        {
          "metric_type": "cpuutil",
          "breach_duration_secs": 120,
          "threshold": 70,
          "operator": ">=",
          "cool_down_secs": 120,
          "adjustment": "+1"
        },
        {
          "metric_type": "cpuutil",
          "breach_duration_secs": 120,
          "threshold": 25,
          "operator": "<",
          "cool_down_secs": 120,
          "adjustment": "-1"
        }
      ]
    }
    ```
 2. Attach the policy:
    ```shell
    cf attach-autoscaling-policy <application name> 'app-policy.json'
    ```
