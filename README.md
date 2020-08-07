# From Alert Notification to Comparison of Good and Bad Requests in One Click

This is a working demo that accompanies the talk "From Alert Notification to Comparison of Good and Bad Requests in One Click" from KubeCon EU 2020's Observability track.

It shows OpenMetrics exporting metrics and exemplar trace IDs, then metrics and exemplars being scraped by Prometheus, forwarded to M3 where exemplars and metrics live in long term storage, and the ability to click on a datapoint in any graph in Grafana and jump straight to the exemplar trace associated with that datapoint. Additionally, it provides the ability to compare a bad trace with a good trace.

All the forked sources and changes are present under https://github.com/chronosphereiox

## Prerequisites

- NodeJS 10.xx
- Go 1.13

The demo checks out the required repositories as sub-modules, builds the docker images and launches
them. Use:
```bash
make start
```
to run this the first time. This will take a while to build as it is building
grafana, prometheus, m3 and a couple of other things.

Once the images are built you can use the following to start and stop the demo.

```bash
make app_start # starts the demo

make app_stop # stops the demo
```

Once the demo is up traverse to http://localhost:8080/ to enable traffic through the demo jaeger app
and have the application emit traces and metrics.

The demo automatically provisions an M3Query data source and a sample grafana dashboard that shows 
a request success/failure metric with traces linked to individual datapoints if present. When you 
click on a datapoint in the series, if there is an associated trace the `Show Trace` button will 
take you to the jaeger view of that specific trace and span and the `Show Diff` button will take you
to a trace difference between a good and a bad trace.
