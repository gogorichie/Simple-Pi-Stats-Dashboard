# SimplePi Stats

![screenshot](https://github.com/gogorichie/Simple-Pi-Stats-Dashboard/blob/master/Dashboard.jpg)

This is a quick and easy to understand dashboard for monitoring the performance of your Raspberry Pi devices.

## Dependencies:
* [GRAFANA](https://grafana.com/) 
* GRAPH 
* [INFLUXDB](https://www.influxdata.com/products/influxdb-overview/)
* SINGLESTAT

## Collector:
* [Telegraf](https://www.influxdata.com/time-series-platform/telegraf/)

###############################################################################
#                            INPUT PLUGINS                                    #
###############################################################################

<br /> [[inputs.net]]
<br /> [[inputs.netstat]]
<br /> [[inputs.disk]]
<br /> [[inputs.cpu]]
<br />   percpu = true
<br />   totalcpu = true
<br />   collect_cpu_time = false
<br />   report_active = false
<br /> [[inputs.diskio]]
<br /> [[inputs.kernel]]
<br /> [[inputs.mem]]
<br /> [[inputs.processes]]
<br /> [[inputs.swap]]
<br /> [[inputs.system]]
<br /> [[inputs.internal]]
<br /> [[inputs.interrupts]]
<br />    cpu_as_tag = true
<br /> [[inputs.linux_sysctl_fs]]

![GitHub last commit](https://img.shields.io/github/last-commit/gogorichie/Simple-Pi-Stats-Dashboard?style=for-the-badge)
[![GitHub](https://img.shields.io/github/license/gogorichie/Simple-Pi-Stats-Dashboard?style=for-the-badge)](LICENCE)
