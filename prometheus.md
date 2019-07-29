Prometheus监控
===

### Golang接入
```go
import (
    std "gitlab.wallstcn.com/wscnbackend/ivankastd"
    "github.com/micro/go-os/metrics"
    "time"
    "gitlab.wallstcn.com/wscnbackend/ivankastd/service/metrics/prometheus"
)

func main() {
    metric := newMetrics(conf)
    pushSuccessCounter := metric.Counter("push_success_total")
    pushFailureCounter := metric.Counter("push_failure_total")

    // Increment one push success
    pushSuccessCounter.WithFields(metrics.Fields{
        "url": "https://pushsuccess.com",
    }).Incr(1)

    // Increment one push failure
    pushFailureCounter.WithFields(metrics.Fields{
        "url": "https://pushfailure.com",
    }).Incr(1)
}

func newMetrics(conf std.ConfigPrometheus) metrics.Metrics {
	options := make([]metrics.Option, 0)
	options = append(options, metrics.WithFields(metrics.Fields{
		"url": "",
	}))
	if conf.Namespace != "" {
		options = append(options, metrics.Namespace(conf.Namespace))
	}
	if conf.BatchInterval > 0 {
		options = append(options, metrics.BatchInterval(time.Duration(conf.BatchInterval)))
	}
	if len(conf.Collectors) > 0 {
		addrs := make([]string, 0, len(conf.Collectors))
		for _, col := range conf.Collectors {
			addrs = append(addrs, col.Addr)
		}
		options = append(options, metrics.Collectors(addrs...))
	}
	return prometheus.NewMetrics(options...)
}
```
