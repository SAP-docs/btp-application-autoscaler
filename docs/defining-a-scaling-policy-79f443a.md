<!-- loio79f443abe6b448ce9b606d10fd816f5c -->

# Defining a Scaling Policy

Define a policy to scale your application instances either dynamically or based on schedules.

To initiate the scaling of an application, you need to define a policy. A policy is a JSON file containing an array of rules or a single rule for scaling. This JSON file is passed while binding the service with the application to be scaled. For more information, see [Initial Setup](initial-setup-f3e7fa9.md).

You can choose between the following types of scaling policies:

-   [**Dynamic Scaling Policy**](dynamic-scaling-policy-e6927e5.md)

    Scale your application instances based on memory/CPU usage, reponse time, throughput, or custom metrics.

-   [**Schedule-Based Scaling Policy**](schedule-based-scaling-policy-204e423.md)

    Scale your application instances based on schedules.


**Related Information**  


[Parameters for a Dynamic Scaling Policy](parameters-for-a-dynamic-scaling-policy-c966417.md "Get to know the parameters used for dynamic scaling.")

[Parameters for a Schedule-Based Scaling Policy](parameters-for-a-schedule-based-scaling-policy-c8023eb.md "Get to know the parameters used for recurring schedules or specific date schedules.")

[Time Zones for a Schedule-Based Policy](time-zones-for-a-schedule-based-policy-92bceeb.md "Get to know the time zones supported for recurring schedules or specific date schedules.")

