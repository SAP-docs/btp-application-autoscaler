<!-- loio3ff73fce08b44e8d8de0c102d0f64a50 -->

# Working with the Application Autoscaler Dashboard

Access and use the Application Autoscaler dashboard.

<a name="loio9397913bcf10438e91bfda6a852fcac4"/>

<!-- loio9397913bcf10438e91bfda6a852fcac4 -->

## Access the Application Autoscaler Dashboard

Access the Application Autoscaler dashboard, which lets you create or update a scaling policy, and view the scaling details.



<a name="loio9397913bcf10438e91bfda6a852fcac4__prereq_ysy_wd4_hdb"/>

## Prerequisites

You have created an Application Autoscaler service instance and bound it to your application. See [Initial Setup](initial-setup-f3e7fa9.md).



## Procedure

1.  In the SAP BTP cockpit, navigate to the *Organization* \> *Space* containing the Application Autoscaler.

2.  From the navigation pane, choose *Service Marketplace*.

3.  Choose *Application Autoscaler*.

4.  In the navigation pane, choose *Instances*.

    The list of created instances appears.

5.  From the *Actions* column, choose \(Open Dashboard\).

6.  Provide the platform credentials to access the dashboard.

    The *Overview* page appears.

7.  In the navigation pane, choose *Referencing Apps*.

    The list of applications bound to the service instance appears. In the *Actions* column, the *Manage Policy* and *Scaling History* options are available.


<a name="loiod634ef0d78ce4e6f87689fd4abdecc5a"/>

<!-- loiod634ef0d78ce4e6f87689fd4abdecc5a -->

## Use the Application Autoscaler Dashboard

Manage your scaling policy and view the scaling history.



The Application Autoscaler dashboard comprises two features, which let you perform different actions: *Manage Policy* and *Scaling History*.



### Manage Policy

A scaling policy defines the scaling requirements of an application. *Manage Policy* lets you perform the following tasks:

-   *Create a Policy*

    Define scaling requirements if you haven’t used configuration parameters with the bind request during the binding of the service with an application.

-   *View a Policy*

    Preview your policy, especially if you’ve defined it during the binding process.

-   *Edit a Policy*

    Change an existing policy, for example to:

    -   Add more scaling rules
    -   Add schedule-based scaling along with dynamic scaling
    -   Update scaling parameters like cool down and threshold adjustment based on their behavior as observed in the *Scaling History* feature.


For information about scaling policy, see [Dynamic Scaling Policy](dynamic-scaling-policy-e6927e5.md).



### Scaling History

This feature lists all scaling events that were triggered by the Application Autoscaler service instance after it was bound to an application. The scaling history helps you to troubleshoot and resolve issues if the scaling doesn’t match the defined policy.

> ### Example:  
> If the scaling failed due to quota restrictions, an appropriate message is displayed in the scaling history. Accordingly, you can request additional quota.

