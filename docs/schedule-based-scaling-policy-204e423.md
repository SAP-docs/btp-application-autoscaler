<!-- loio204e423225054588a08771f8190ac9aa -->

# Schedule-Based Scaling Policy

Scale your application instances based on schedules.

You can either define recurring schedules or specific date schedules for scaling. If you want to define multiple schedules, make sure that they don't overlap.

> ### Caution:  
> Overlapping schedules don't trigger the scaling.

In recurring schedules, the date is optional. However, you need to provide a date for a specific date schedule. If you set the parameters `instance_min_count` and `instance_max_count` within a schedule, they override the global values set for these parameters.



<a name="loio204e423225054588a08771f8190ac9aa__section_anf_g3g_n4b"/>

## Recurring Schedules

The following example shows a schedule-based scaling policy:

> ### Sample Code:  
> ```
> 
> {
>  "instance_min_count": 1, 
>  "instance_max_count": 5, 
>    "schedules": {  
>    "timezone":"Asia/Shanghai",
>    "recurring_schedule":[  
>       {  
>          "start_time":"10:00",
>          "end_time":"18:00",
>          "days_of_week":[  
>             1,
>             2,
>             3
>          ],
>          "instance_min_count":1,
>          "instance_max_count":10,
>          "initial_min_instance_count":5
>       }      
>      ]
>    }
> }
> ```

The policy in the example defines a recurring schedule, which is set for the Asia/Shanghai time zone. The schedule triggers application instances during the specified time frame on Sunday, Monday, and Tuesday. The days of the week are specified through the numbers 1 to 7 starting with 1 for Monday.

The policy defines the minimum and maximum number of application instances during the time frame as well as the number of application instances that should be available at the beginning of the recurring schedule.

For more information about the time zones for schedule-based policies, see [Time Zones for a Schedule-Based Policy](time-zones-for-a-schedule-based-policy-92bceeb.md).



<a name="loio204e423225054588a08771f8190ac9aa__section_acl_l3g_n4b"/>

## Schedules with Start Day and Day of the Month, and Specific Date Schedules

The following examples show schedule-based scaling with start date and day of the month, as well as a specific date schedule.


<table>
<tr>
<th valign="top">

Schedule with Start Date and Day of the Month

</th>
<th valign="top">

Specific Date Schedule

</th>
</tr>
<tr>
<td valign="top">

> ### Sample Code:  
> ```
> "schedules": {  
>    "timezone":"Asia/Shanghai",
>    "recurring_schedule":[  
>        {  
>          "start_date":"2016-06-27",
>          "end_date":"2016-07-23",
>          "start_time":"11:00",
>          "end_time":"19:30",
>          "days_of_month":[  
>             5,
>             15,
>             25
>          ],
>          "instance_min_count":3,
>          "instance_max_count":10,
>          "initial_min_instance_count":5
>       }
> 
> ```



</td>
<td valign="top">

> ### Sample Code:  
> ```
> {
>     "instance_min_count": 1, 
>     "instance_max_count": 5, 
>  "schedules":{  
>    "timezone":"Asia/Shanghai",
> "specific_date":[
>           {
>              "start_date_time":"2015-06-02T10:00", 
>              "end_date_time":"2015-06-15T13:59", 
>              "instance_min_count":1,
>              "instance_max_count":4,
>              "initial_min_instance_count":2
>           },
>           {
>              "start_date_time":"2015-01-04T20:00",
>              "end_date_time":"2015-02-19T23:15",
>              "instance_min_count":2,
>              "instance_max_count":5,
>              "initial_min_instance_count":3
>           }
>     ]
>   }
>  }
> ```



</td>
</tr>
</table>



<a name="loio204e423225054588a08771f8190ac9aa__section_n1n_p3g_n4b"/>

## Advanced Usage

For advanced usage, you can provide optional values along with the mandatory ones. The following sample displays such a scaling policy:

> ### Sample Code:  
> ```
> {
>  "instance_min_count": 1, 
>  "instance_max_count": 5, 
>    "schedules": {  
>    "timezone":"Asia/Shanghai",
>    "recurring_schedule":[  
>       {  
>          "start_time":"10:00",
>          "end_time":"18:00",
>          "days_of_week":[  
>             1,
>             2,
>             3
>          ],
>          "instance_min_count":1,
>          "instance_max_count":10,
>          "initial_min_instance_count":5
>       },
>       {  
>          "start_date":"2016-06-27",
>          "end_date":"2016-07-23",
>          "start_time":"11:00",
>          "end_time":"19:30",
>          "days_of_month":[  
>             5,
>             15,
>             25
>          ],
>          "instance_min_count":3,
>          "instance_max_count":10,
>          "initial_min_instance_count":5
>        }
>      ]
>    }
> }
> ```

For more information about the parameters used, see [Parameters for a Schedule-Based Scaling Policy](parameters-for-a-schedule-based-scaling-policy-c8023eb.md).

**Related Information**  


[Parameters for a Schedule-Based Scaling Policy](parameters-for-a-schedule-based-scaling-policy-c8023eb.md "Get to know the parameters used for recurring schedules or specific date schedules.")

[Time Zones for a Schedule-Based Policy](time-zones-for-a-schedule-based-policy-92bceeb.md "Get to know the time zones supported for recurring schedules or specific date schedules.")

