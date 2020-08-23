# SimplePi Stats

![screenshot](https://github.com/gogorichie/Simple-Pi-Stats-Dashboard/blob/master/Dashboard.jpg)

This is a quick and easy to understand dashboard monitoring the performance of your RaspberryPi devices.

## Dependencies:
* GRAFANA
* GRAPH
* INFLUXDB
* SINGLESTAT

## Collector:
* Telegraf

###############################################################################
#                            INPUT PLUGINS                                    #
###############################################################################

<br /> [[inputs.net]]
<br /> [[inputs.netstat]]
<br /> [[inputs.disk]]
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
<br /> [[inputs.net]]
<br /> [[inputs.netstat]]
