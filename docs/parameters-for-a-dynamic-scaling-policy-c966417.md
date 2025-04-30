<!-- loioc96641745df24fd88d8c84812bf07837 -->

# Parameters for a Dynamic Scaling Policy

Get to know the parameters used for dynamic scaling.




<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Description

</th>
<th valign="top">

Mandatory

</th>
<th valign="top">

Data Type

</th>
<th valign="top">

Value Range

</th>
<th valign="top">

Default Value

</th>
<th valign="top">

Example

</th>
</tr>
<tr>
<td valign="top">

`instance_min_count` 

</td>
<td valign="top">

The minimum number of application instances that are always running.

</td>
<td valign="top">

Yes

</td>
<td valign="top">

number

</td>
<td valign="top">

minimum = 1; maximum = no upper limit

</td>
<td valign="top">

none

</td>
<td valign="top">

`1` 

</td>
</tr>
<tr>
<td valign="top">

`instance_max_count` 

</td>
<td valign="top">

The maximum number of application instances that can be provisioned as part of application scaling.

</td>
<td valign="top">

Yes

</td>
<td valign="top">

number

</td>
<td valign="top">

minimum = `instance_min_count`; maximum = no upper limit

</td>
<td valign="top">

none

</td>
<td valign="top">

`5` 

</td>
</tr>
<tr>
<td valign="top">

`scaling_rules` 

</td>
<td valign="top">

A rule comprises a group of key values set to automatically trigger the scaling activity. You can have one or more rules. At least one rule out of a possible array size of two is validated.

</td>
<td valign="top">

Yes

</td>
<td valign="top">

array

</td>
<td valign="top">

none

</td>
<td valign="top">

none

</td>
<td valign="top">

none

</td>
</tr>
<tr>
<td valign="top">

`metric_type` 

</td>
<td valign="top">

The metric type can be one of the following options:

-   memory usage in mebibytes \(`memoryused`\)

-   memory utilization as a percentage of the memory quota \(`memoryutil`\)

-   CPU as a percentage of virtual CPUs used \(`cpu`\)

    > ### Tip:  
    > Instead, we recommend to use the CPU entitlement utilization metric \(`cpuutil`\), which eliminates the need to calculate the CPU entitlement for your application.

-   CPU entitlement utilization as percentage \(`cpuutil`\)
-   disk usage in mebibytes \(`disk`\)

-   disk utilization as a percentage of the disk quota \(`diskutil`\)

-   throughput in requests per second \(`throughput`\)

-   response time in milliseconds \(`responsetime`\)



</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

none

</td>
<td valign="top">

none

</td>
<td valign="top">

One of the following options:

-   `memoryused`

-   `memoryutil`

-   `cpu`

-   `cpuutil`

-   `disk`

-   `diskutil`

-   `throughput`

-   `responsetime`




</td>
</tr>
<tr>
<td valign="top">

`breach_duration_secs` 

</td>
<td valign="top">

The duration to analyze the collected metrics data points. The duration is considered from the current time to the past, for example: the last 600 seconds.

The service performs this analysis to check if the data points are consistently above or below the set threshold and makes the decision to scale. For a more accurate decision, set a larger duration, as in this case, more data points are analyzed.

In situations that cause a rapid increase of application load in short intervals, set a small duration. This enables the application to scale out before the maximum memory threshold is exceeded and prevents the application from crashing.

</td>
<td valign="top">

No

</td>
<td valign="top">

number

</td>
<td valign="top">

minimum = 60 seconds; maximum = 3600 seconds

</td>
<td valign="top">

300 seconds

</td>
<td valign="top">

`300 seconds` 

</td>
</tr>
<tr>
<td valign="top">

`threshold` 

</td>
<td valign="top">

The threshold is compared to one of the following options:

-   memory usage in mebibytes \(metric type `memoryused`\)

-   memory utilization as a percentage of the memory quota \(metric type `memoryutil`\)

-   CPU usage as a percentage of virtual CPUs used \(metric type `cpu`\)

-   CPU entitlement utilization as percentage \(metric type `cpuutil`\)

-   disk usage in mebibytes \(metric type `disk`\)

-   disk utilization as a percentage of the disk quota \(metric type `diskutil`\)

-   throughput in requests per second \(metric type `throughput`\)

-   response time in milliseconds \(metric type `responsetime`\)




</td>
<td valign="top">

Yes

</td>
<td valign="top">

integer

</td>
<td valign="top">

-   `memoryused`: minimum = 1; maximum = no upper limit

-   `memoryutil`: minumum = 1; maximum = 100
-   `cpu`: minimum = 1; maximum = 400

-   `cpuutil`: minimum = 1; maximum = 100

-   `disk`: minimum = 1; maximum = 10240

-   `diskutil`: minimum = 1; maximum = 100

-   `throughput`: minimum = 1; maximum = no upper limit

-   `responsetime`: minimum = 1; maximum = no upper limit




</td>
<td valign="top">

none

</td>
<td valign="top">

`30` 

</td>
</tr>
<tr>
<td valign="top">

`operator` 

</td>
<td valign="top">

The operator is used in combination with the threshold value to compare the current metric value. The expression is as follows: `[MetricUsage value] [operator] [threshold]`.

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

<

\>

<=

\>=

</td>
<td valign="top">

none

</td>
<td valign="top">

`64 > 30` 

</td>
</tr>
<tr>
<td valign="top">

`cool_down_secs` 

</td>
<td valign="top">

The minimum duration between two successive scaling actions.

After this scaling has been initiated, the next scaling action can only occur after this specified interval. During this interval, no other scaling action can be initiated.

This interval ensures the application remains stable before initiating another scaling action. For production environments, it is recommended to set a longer interval.

</td>
<td valign="top">

No

</td>
<td valign="top">

number

</td>
<td valign="top">

minimum = 60 seconds; maximum = 3600 seconds

</td>
<td valign="top">

300 seconds

</td>
<td valign="top">

`300` 

</td>
</tr>
<tr>
<td valign="top">

`adjustment` 

</td>
<td valign="top">

The number of application instances to be scaled as part of the scaling activity. The format is `+` or `-` followed by one of the following:

-   the number of required instances

-   the number of required instances followed by a percentage sign \(*%*\)

    The number is then divided by 100 and multiplied with the number of application instances currently running to determine the final adjustment amount.




</td>
<td valign="top">

Yes

</td>
<td valign="top">

number

</td>
<td valign="top">

none

</td>
<td valign="top">

none

</td>
<td valign="top">

-   `+1` to scale up by an instance; `-2` to scale down by two instances

-   `+100%` to double the number of instances; `-50%` to halve the number of instances




</td>
</tr>
</table>

**Related Information**  


[Dynamic Scaling Policy](dynamic-scaling-policy-e6927e5.md "Scale your application instances based on memory or CPU usage, response time, throughput, or custom metrics.")

