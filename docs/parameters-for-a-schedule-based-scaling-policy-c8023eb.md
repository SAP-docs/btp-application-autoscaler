<!-- loioc8023eb0995e42a68697f4262218a032 -->

# Parameters for a Schedule-Based Scaling Policy

Get to know the parameters used for recurring schedules or specific date schedules.




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

`schedules` 

</td>
<td valign="top">

A schedule lets you configure scaling rules for specific days or on a recurring basis. Schedules guard against expected high surges or low activity periods.

</td>
<td valign="top">

Yes

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
<td valign="top">

none

</td>
</tr>
<tr>
<td valign="top">

`timezone` 

</td>
<td valign="top">

A valid time zone to run the schedule. For more information, see [Time Zones for a Schedule-Based Policy](time-zones-for-a-schedule-based-policy-92bceeb.md).

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

`Asia/Sanghai` 

</td>
</tr>
<tr>
<td valign="top">

`recurring_schedule` 

</td>
<td valign="top">

Triggers the scaling rule recursively during the specified intervals

</td>
<td valign="top">

Yes

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
<td valign="top">

none

</td>
</tr>
<tr>
<td valign="top">

`start_time` 

</td>
<td valign="top">

Start time of a recurring schedule in 24-hr format \(HH:MM\).

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

minimum = 00:00; maximum = 23:59

</td>
<td valign="top">

none

</td>
<td valign="top">

`10:00` 

</td>
</tr>
<tr>
<td valign="top">

`end_time` 

</td>
<td valign="top">

End time of a recurring schedule in 24-hr format \(HH:MM\).

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

minimum = 00:00; maximum = 23:59

</td>
<td valign="top">

none

</td>
<td valign="top">

`21:00` 

</td>
</tr>
<tr>
<td valign="top">

`start_date` 

</td>
<td valign="top">

Start date of the schedule in YYYY-MM-DD format.

</td>
<td valign="top">

No

</td>
<td valign="top">

string

</td>
<td valign="top">

minimum = current date; maximum = no upper limit

</td>
<td valign="top">

none

</td>
<td valign="top">

`2020-06-27` 

</td>
</tr>
<tr>
<td valign="top">

`end_date` 

</td>
<td valign="top">

End date of the schedule in YYYY-MM-DD format.

</td>
<td valign="top">

No

</td>
<td valign="top">

string

</td>
<td valign="top">

minimum = set by start\_date; maximum = no upper limit

</td>
<td valign="top">

none

</td>
<td valign="top">

`2020-07-23` 

</td>
</tr>
<tr>
<td valign="top">

`days_of_week` 

</td>
<td valign="top">

Triggers the scaling on weekdays ranging from 1 \(Monday\) to 7 \(Sunday\). The rule is executed during the weekdays specified within the array.

</td>
<td valign="top">

Yes

</td>
<td valign="top">

array

</td>
<td valign="top">

minimum = 1; maximum = 7

</td>
<td valign="top">

none

</td>
<td valign="top">

`[1,3,5]` 

</td>
</tr>
<tr>
<td valign="top">

`days_of_month` 

</td>
<td valign="top">

Triggers the scaling on days of the month ranging from 1 to 31. The rule is executed during the specified days of the month.

</td>
<td valign="top">

Yes

</td>
<td valign="top">

array

</td>
<td valign="top">

minimum = 1; maximum = 31

</td>
<td valign="top">

none

</td>
<td valign="top">

`[1,11,24,30]` 

</td>
</tr>
<tr>
<td valign="top">

`instance_min_count` 

</td>
<td valign="top">

Minimum number of instances during the recurrence period.

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

Maximum number of instances during the recurrence period.

</td>
<td valign="top">

Yes

</td>
<td valign="top">

number

</td>
<td valign="top">

minimum = set by `instance_min_count`; maximum = no upper limit

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

`initial_min_instance_count` 

</td>
<td valign="top">

Minimum number of instances to scale up at the beginning of the recurrence period.

</td>
<td valign="top">

Yes

</td>
<td valign="top">

number

</td>
<td valign="top">

minimum = set by `instance_min_count`; maximum = `instance_max_count` 

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

`specific_date` 

</td>
<td valign="top">

Triggers the scaling rule during the specified date intervals.

</td>
<td valign="top">

Yes

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
<td valign="top">

none

</td>
</tr>
<tr>
<td valign="top">

`start_date_time` 

</td>
<td valign="top">

Start date and time of the schedule in YYYY-MM-DDTHH:MM format

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

minimum = current date and time; maximum= no upper limit

</td>
<td valign="top">

none

</td>
<td valign="top">

`2015-06-02 T10:00` 

</td>
</tr>
<tr>
<td valign="top">

`end_date_time` 

</td>
<td valign="top">

End date and time of the schedule in YYYY-MM-DDTHH:MM format

</td>
<td valign="top">

Yes

</td>
<td valign="top">

string

</td>
<td valign="top">

minimum = set by `start_date_time`; maximum= no upper limit

</td>
<td valign="top">

none

</td>
<td valign="top">

`2015-09-02 T10:00` 

</td>
</tr>
</table>

**Related Information**  


[Schedule-Based Scaling Policy](schedule-based-scaling-policy-204e423.md "Scale your application instances based on schedules.")

[Time Zones for a Schedule-Based Policy](time-zones-for-a-schedule-based-policy-92bceeb.md "Get to know the time zones supported for recurring schedules or specific date schedules.")

