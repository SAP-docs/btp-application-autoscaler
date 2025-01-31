# Plug-in for the “Cloud Foundry CLI”
Application Autoscaler offers a plug-in for the “Cloud Foundry CLI”. With it users can attach or detach scaling-policies to their apps. They can view them and view the scaling-history. And they can view the metrics send by their apps.

This is useful to get some insights on how currently applied scaling-policies work and if changes are reasonable. It is as well useful for debugging. A common case is, when [custom-metrics](<../defining-a-custom-metric-87e657e.md>) are introduced to scale an app and the developers want to check, if the send metrics are correctly processed by Autoscaler and why up-/down-scaling happens or does not happen.
