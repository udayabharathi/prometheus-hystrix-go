# prometheus-hystrix-go

<p align="left">
<a href="https://hits.seeyoufarm.com"/><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fgjbae1212%2Fprometheus-hystrix-go"/></a>
<a href="/LICENSE"><img src="https://img.shields.io/badge/license-MIT-GREEN.svg" alt="license" /></a>
<a href="https://goreportcard.com/report/github.com/gjbae1212/prometheus-hystrix-go"><img src="https://goreportcard.com/badge/github.com/gjbae1212/prometheus-hystrix-go" alt="Go Report Card" /></a> 
</p>

## OVERVIEW
**prometheus-hystrix-go** is metric collector of prometheus for [hystrix-go](https://github.com/afex/hystrix-go)

## HOW TO USE
```go
package main

import (
	"net/http"
	hystrix_metric "github.com/afex/hystrix-go/hystrix/metric_collector"
	prometheus_hystrix_go "github.com/gjbae1212/prometheus-hystrix-go"
	"github.com/prometheus/client_golang/prometheus/promhttp"
)

func main() {
    // get wrapper of prometheus metric collector.
	wrapper := prometheus_hystrix_go.NewPrometheusCollector("your prometheus namespace", "your prometheus subsystem")

	// register and initialize the collector.
	hystrix_metric.Registry.Register(wrapper)
	hystrix_metric.Registry.InitializeMetricCollectors("")

	// start server
	http.Handle("/metrics", promhttp.Handler())
	http.ListenAndServe(":8080", nil)
}
```
this example allows you get to the prometheus metric of the hystrix when you request to `/metrics` path  


### LICENSE
This project is following The MIT.
