# SimplePi Stats

![screenshot](https://github.com/gogorichie/Simple-Pi-Stats-Dashboard/blob/master/Dashboard.jpg)

This is a quick and easy to understand dashboard for monitoring the performance of your RaspberryPi devices.

## Dependencies:
* [GRAFANA](https://grafana.com/) 
* GRAPH 
* [INFLUXDB](https://www.influxdata.com/products/influxdb-overview/)
* SINGLESTAT

## Collector:
* [Telegraf](https://www.influxdata.com/time-series-platform/telegraf/)

[global_tags]
[agent]
  interval = "10s"
  round_interval = true
  metric_batch_size = 1000
  metric_buffer_limit = 10000
  collection_jitter = "0s"
  flush_jitter = "0s"
  precision = ""
  hostname = ""
  omit_hostname = false


###############################################################################
#                            OUTPUT PLUGINS                                   #
###############################################################################
[[outputs.influxdb]]
 urls = ["http://local:8086"]

###############################################################################
#                            INPUT PLUGINS                                   #
###############################################################################

[[inputs.net]]
[[inputs.netstat]]
[[inputs.disk]]
[[inputs.cpu]]
  percpu = true
  totalcpu = true
  collect_cpu_time = false
  report_active = false
[[inputs.diskio]]
[[inputs.kernel]]
[[inputs.mem]]
[[inputs.processes]]
[[inputs.swap]]
[[inputs.system]]
[[inputs.internal]]
[[inputs.interrupts]]
  cpu_as_tag = true
[[inputs.linux_sysctl_fs]]
