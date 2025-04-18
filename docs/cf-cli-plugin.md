# Application Autoscaler Plugin for the Cloud Foundry CLI
The Application Autoscaler offers a plugin for the Cloud Foundry Command Line Interface CLI. The plugin enables users to:
  * attach or detach scaling policies to apps
  * view attached scaling policies and view the scaling histories
  * view the metrics sent by apps

This is useful:
  * to get some insights into how current scaling policies work and if changes are reasonable.
  * for debugging, especially when introducing [custom-metrics](<../defining-a-custom-metric-87e657e.md>) to scale an app. It lets you check if the sent metrics are correctly handled by the Application Autoscaler, and it helps you understand why your app is scaling out or in or why this does not happen.

This documentation explains how to use the plugin on Cloud Foundry in BTP. For details not related to BTP, see  <https://github.com/cloudfoundry/app-autoscaler-cli-plugin/blob/main/README.md>.

## Command List
| Command                                                          | Description                                             |
|------------------------------------------------------------------|---------------------------------------------------------|
| [autoscaling-policy, asp](#cf-autoscaling-policy)                | Retrieve the scaling policy of an application           |
| [attach-autoscaling-policy, aasp](#cf-attach-autoscaling-policy) | Attach a scaling policy to an application               |
| [detach-autoscaling-policy, dasp](#cf-detach-autoscaling-policy) | Detach the scaling policy from an application           |
| [autoscaling-metrics, asm](#cf-autoscaling-metrics)              | Retrieve the metrics of an application                  |
| [autoscaling-history, ash](#cf-autoscaling-history)              | Retrieve the scaling history of an application          |

## Command usage
### `cf autoscaling-policy`
Retrieve the scaling policy of an application, the policy will be displayed in JSON format.
```shell
cf autoscaling-policy APP_NAME [--output PATH_TO_FILE]
```

> #### Alias:
> asp


#### Options:
- `--output` : dump the policy to a file in JSON format

#### Examples:
- View scaling policy, replace `APP_NAME` with the name of your application:
  ```shell
  $ cf autoscaling-policy APP_NAME

  Showing policy for app APP_NAME...
  {
      "instance_min_count": 1,
      "instance_max_count": 5,
      "scaling_rules": [
          {
              "metric_type": "memoryused",
              "breach_duration_secs": 120,
              "threshold": 15,
              "operator": ">=",
              "cool_down_secs": 120,
              "adjustment": "+1"
          },
          {
              "metric_type": "memoryused",
              "breach_duration_secs": 120,
              "threshold": 10,
              "operator": "<",
              "cool_down_secs": 120,
              "adjustment": "-1"
          }
      ]
  }
  ```
- Dump the scaling policy to a file in JSON format:
  ```shell
  $ cf asp APP_NAME --output PATH_TO_FILE

  Saving policy for app APP_NAME to PATH_TO_FILE...
  OK
  ```

### `cf attach-autoscaling-policy`
Attach a scaling policy to an application. The policy file must be a JSON file. See [policy specification](<./defining-a-scaling-policy-79f443a.md>) for the policy format.

```shell
cf attach-autoscaling-policy APP_NAME PATH_TO_POLICY_FILE
```

> #### Alias:
> aasp

#### Examples:
```shell
$ cf attach-autoscaling-policy APP_NAME PATH_TO_POLICY_FILE

Attaching policy for app APP_NAME...
OK
```

### `cf detach-autoscaling-policy`
Detach the scaling policy from an application. The policy will be **deleted** when detached.
```shell
cf detach-autoscaling-policy APP_NAME
```

> #### Alias: dasp

#### Examples:
```shell
$ cf detach-autoscaling-policy APP_NAME

Detaching policy for app APP_NAME...
OK
```

### `cf autoscaling-metrics`
Retrieve the aggregated metrics of an application. You can specify the start/end time of the returned query result and the display order (ascending or descending). The metrics are shown in a table.
```shell
cf autoscaling-metrics APP_NAME METRIC_NAME [--start START_TIME] [--end END_TIME] [--asc] [--output PATH_TO_FILE]
```

> #### Alias:
> asm

#### Options:
- `METRIC_NAME` : default metrics "memoryused, memoryutil, responsetime, throughput, cpu" or customized name for your own metrics.
- `--start` : start time of metrics collected with format `yyyy-MM-ddTHH:mm:ss+/-HH:mm` or `yyyy-MM-ddTHH:mm:ssZ`, default to very beginning if not specified.
- `--end` : end time of the metrics collected with format `yyyy-MM-ddTHH:mm:ss+/-HH:mm` or `yyyy-MM-ddTHH:mm:ssZ`, default to current time if not speficied.
- `--asc` : display in ascending order, default to descending order if not specified
- `--output` : dump the metrics to a file

#### Examples:
```shell
$ cf autoscaling-metrics APP_NAME memoryused --start 2018-12-27T11:49:00+08:00 --end 2018-12-27T11:52:20+08:00 --asc

Retriving aggregated metrics for app APP_NAME...
Metrics Name        Value       Timestamp
memoryused          62MB        2018-12-27T11:49:00+08:00
memoryused          62MB        2018-12-27T11:49:40+08:00
memoryused          61MB        2018-12-27T11:50:20+08:00
memoryused          62MB        2018-12-27T11:51:00+08:00
memoryused          62MB        2018-12-27T11:51:40+08:00
```
- `Metrics Name`: name of the current metric item
- `Value`: the value of the current metric item with unit
- `Timestamp`: collect time of the current metric item

### `cf autoscaling-history`
Retrieve the scaling event history of an application. You can specify the start/end time of the returned query result, and the display order (ascending or descending). The scaling event history is shown in a table.
```shell
cf autoscaling-history APP_NAME [--start START_TIME] [--end END_TIME] [--asc] [--output PATH_TO_FILE]
```

> #### Alias:
> ash

#### Options:
- `--start` : start time of the scaling history with format `yyyy-MM-ddTHH:mm:ss+/-HH:mm` or `yyyy-MM-ddTHH:mm:ssZ`, default to very beginning if not specified.
- `--end` : end time of the scaling history with format `yyyy-MM-ddTHH:mm:ss+/-HH:mm` or `yyyy-MM-ddTHH:mm:ssZ`, default to current time if not speficied.
- `--asc` : display in ascending order, default to descending order if not specified
- `--output` : dump the scaling history to a file

#### Examples:
```shell
$ cf autoscaling-history APP_NAME --start 2018-08-16T17:58:53+08:00 --end 2018-08-16T18:01:00+08:00 --asc

Showing history for app APP_NAME...
Scaling Type        Status          Instance Changes        Time                            Action                                                          Error
dynamic             failed          2->-1                   2018-08-16T17:58:53+08:00       -1 instance(s) because throughput < 10rps for 120 seconds       app does not have policy set
dynamic             succeeded       2->3                    2018-08-16T17:59:33+08:00       +1 instance(s) because memoryused >= 15MB for 120 seconds
scheduled           succeeded       3->6                    2018-08-16T18:00:00+08:00       3 instance(s) because limited by min instances 6
```

#### Description of table-columns:
- `Scaling Type`: the trigger type of the scaling action, possible scaling types: `dynamic` and `scheduled`
  - `dynamic`: the scaling action is triggered by a dynamic rule (memoryused, memoryutil, responsetime or throughput)
  - `scheduled`: the scaling action is triggered by a recurring schedule or specific date rule
- `Status`: the result of the scaling action: `succeeded` or `failed`
- `Instance Changes`: how the instances number get changed (e.g. `1->2` means the application was scaled out from 1 instance to 2)
- `Time`: the finish time of scaling action, no mater succeeded or failed
- `Action`: the detail information about why and how the application scaled
- `Error`: the reason why scaling failed
