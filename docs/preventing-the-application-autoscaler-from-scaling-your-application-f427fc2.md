<!-- loiof427fc283599432bb39684307fd082c6 -->

# Preventing the Application Autoscaler from Scaling your Application

You want to prevent the Application Autoscaler from scaling your application without unbinding it from the Application Autoscaler service instance or deleting the scaling policy.



<a name="loiof427fc283599432bb39684307fd082c6__prereq_ey5_wrh_jdc"/>

## Prerequisites

-   You have set up autoscaling \(by binding your application to an Application Autoscaler service instance\) and a scaling policy.

-   You are a Space Developer in the space where your application is running.




## Context

For example, during a deployment or maintenance of your application you want to manually control the scaling of your application \(and prevent the Application Autoscaler from automatically scaling your application\) without changing the setup of your application.



## Procedure

Set the label `app-autoscaler.cloudfoundry.org/disable-autoscaling` on your application.

> ### Sample Code:  
> ```
> cf set-label app <application name> app-autoscaler.cloudfoundry.org/disable-autoscaling=<any non-empty string value>
> ```

 > ### Note:  
> -   You can set the value of the label`app-autoscaler.cloudfoundry.org/disable-autoscaling` to any non-empty value. We recommend to use a value that can be used to later determine the reason why it was set.
> 
> -   Other applications or services might set the label as well. For example, the SAP Cloud Deployment service sets and removes the label during a deployment to be able to completely control the scaling during a deployment. For more information, see[\(Experimental\) Incremental Blue-Green Deployment Strategy](https://help.sap.com/docs/BTP/65de2977205c403bbc107264b8eccf4b/2e4dfeded960446da4aa1c0b734fc81b.html?locale=en-US&state=PRODUCTION&version=Cloud).

 