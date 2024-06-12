<!-- loioe6927e5af85e45f4a8a056c8662fa784 -->

# Dynamic Scaling Policy

Scale your application instances based on memory or CPU usage, response time, throughput, or custom metrics.

> ### Note:  
> Both built-in and custom metrics are collected from each application instance individually. Then, their average for all application instances is determined. Based on these average metrics, scaling rules are evaluated once per app.



<a name="loioe6927e5af85e45f4a8a056c8662fa784__section_dtl_yfb_n4b"/>

## Metric Types **memory consumed** and **memory utilized**

These scaling rules define that if the memory consumption either exceeds or falls below the set threshold, the application is respectively scaled up or down by an instance. If an array of scaling rules is defined, the Application Autoscaler runs periodic checks of the scaling policy to verify if any of the specified conditions matches. New instances are generated based on specified rules.

> ### Example:  
> A scaling policy comprises two rules:
> 
> -   Rule 1: If the memory exceeds 500 MB, a single instance of an application is created.
> 
> -   Rule 2: If the memory exceeds 800 MB, two application instances are created.
> 
> 
> When defining an array of rules, its sequence must match the descending order of the threshold values, so that the higher value appears first in the sequence. In this example, rule 2 must be defined before rule 1 to ensure that the Application Autoscaler checks all conditions.



The following table provides examples for dynamic scaling policies based on the metric types **memory consumed** and **memory utilized**.


<table>
<tr>
<th valign="top">

Metric Type **memory consumed** 

</th>
<th valign="top">

Metric Type **memory utilized** 

</th>
</tr>
<tr>
<td valign="top">

> ### Sample Code:  
> ```
> {
>     "instance_min_count": 1, 
>     "instance_max_count": 5, 
>     "scaling_rules": [ 
>         {
>             "metric_type": "memoryused",
>             "threshold": 90,
>             "operator": ">=",
>             "adjustment": "+1"
>         },
>  {
>             "metric_type": "memoryused", 
>             "threshold": 30, 
>             "operator": "<", 
>             "adjustment": "-1" 
>         }
>       
>     ]
> }
> ```



</td>
<td valign="top">

> ### Sample Code:  
> ```
> {
>     "instance_min_count": 1, 
>     "instance_max_count": 5, 
>     "scaling_rules": [ 
>        {
>             "metric_type": "memoryutil",
>             "threshold": 90,
>             "operator": ">=",
>             "adjustment": "+1"
>         },
>   {
>             "metric_type": "memoryutil", 
>             "threshold": 30, 
>             "operator": "<", 
>             "adjustment": "-1" 
>         }
>        
>     ]
> }
> ```



</td>
</tr>
</table>



## Metric Types **throughput** and **responsetime**

The following samples are simple scaling policies for the metric types **throughput** and **responsetime**. The scaling rule determines if the throughput or response time exceeds or falls below the set threshold.


<table>
<tr>
<th valign="top">

Metric Type **throughput** 

</th>
<th valign="top">

Metric Type **responsetime** 

</th>
</tr>
<tr>
<td valign="top">

> ### Sample Code:  
> ```
> {
>     "instance_min_count": 1, 
>     "instance_max_count": 5, 
>     "scaling_rules": [ 
>   
>        {
>             "metric_type": "throughput",
>             "threshold": 100, // the throughput value in Requests/second
>             "operator": ">",
>             "adjustment": "+1"
>         },
>         {
>             "metric_type": "throughput",
>             "threshold": 100,
>             "operator": "<=",
>             "adjustment": "-1"
>         }
> 	]
> }
> ```



</td>
<td valign="top">

> ### Sample Code:  
> ```
> {
>     "instance_min_count": 1, 
>     "instance_max_count": 5, 
>     "scaling_rules": [ 
>        {
>             "metric_type": "responsetime",
>             "threshold": 900, // the response time value in milliseconds
>             "operator": ">",
>             "adjustment": "+1"
>         },
>         {
>             "metric_type": "responsetime",
>             "threshold": 900,
>             "operator": "<=",
>             "adjustment": "-1"
>         }
>       ]
>  }
> ```



</td>
</tr>
</table>



<a name="loioe6927e5af85e45f4a8a056c8662fa784__section_svm_3mb_n4b"/>

## Advanced Usage

For advanced usage, you can provide optional values along with the mandatory ones. The following sample displays such a scaling policy:

> ### Sample Code:  
> ```
> {
>     "instance_min_count": 1, 
>     "instance_max_count": 5, 
>     "scaling_rules": [ 
>         {
>             "metric_type": "memoryused",
>             "breach_duration_secs": 600,
>             "threshold": 90,
>             "operator": ">=",
>             "cool_down_secs": 300,
>             "adjustment": "+1"
>         },
>  {
>             "metric_type": "memoryused", 
>             "breach_duration_secs": 600, 
>             "threshold": 30, 
>             "operator": "<", 
>             "cool_down_secs": 300, 
>             "adjustment": "-1" 
>         }
>        
>     ]
> }
> 
> ```

For more information about the parameters used, see [Parameters for a Dynamic Scaling Policy](parameters-for-a-dynamic-scaling-policy-c966417.md).

**Related Information**  


[Parameters for a Dynamic Scaling Policy](parameters-for-a-dynamic-scaling-policy-c966417.md "Get to know the parameters used for dynamic scaling.")

