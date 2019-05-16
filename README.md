# chi-prometheus (Forked*)

[Prometheus](http://prometheus.io) middleware for [chi](https://github.com/go-chi/chi).

This is a port of [negroni-prometheus](https://github.com/zbindenren/negroni-prometheus)
middleware (written by [Rene Zbinden](https://github.com/zbindenren)).

## Why

[Logging v. instrumentation](http://peter.bourgon.org/blog/2016/02/07/logging-v-instrumentation.html)

Instead of logging request times, it is considered best practice to provide an endpoint
for instrumentation tools (like prometheus).

## How to Install our package
    go get github.com/edjumacator/chi-prometheus

## Usage

Take a look at the [example](./example/main.go).

## What do you get

An endpoint with the following information (stripped output):

    # HELP chi_request_duration_milliseconds How long it took to process the request, partitioned by status code, method and HTTP path.
    # TYPE chi_request_duration_milliseconds histogram
    chi_request_duration_milliseconds_bucke{code="OK",method="GET",path="/metrics",service="serviceName",le="300"} 1
    chi_request_duration_milliseconds_bucke{code="OK",method="GET",path="/metrics",service="serviceName",le="1200"} 1
    chi_request_duration_milliseconds_bucke{code="OK",method="GET",path="/metrics",service="serviceName",le="5000"} 1
    chi_request_duration_milliseconds_bucke{code="OK",method="GET",path="/metrics",service="serviceName",le="+Inf"} 1
    chi_request_duration_milliseconds_sum{code="OK",method="GET",path="/metrics",service="serviceName"} 2.003123
    chi_request_duration_milliseconds_count{code="OK",method="GET",path="/metrics",service="serviceName"} 1
    chi_request_duration_milliseconds_bucke{code="OK",method="GET",path="/ok",service="serviceName",le="300"} 0
    chi_request_duration_milliseconds_bucke{code="OK",method="GET",path="/ok",service="serviceName",le="1200"} 0
    chi_request_duration_milliseconds_bucke{code="OK",method="GET",path="/ok",service="serviceName",le="5000"} 2
    chi_request_duration_milliseconds_bucke{code="OK",method="GET",path="/ok",service="serviceName",le="+Inf"} 2
    chi_request_duration_milliseconds_sum{code="OK",method="GET",path="/ok",service="serviceName"} 4747.529026
    chi_request_duration_milliseconds_count{code="OK",method="GET",path="/ok",service="serviceName"} 2
    # HELP chi_requests_total How many HTTP requests processed, partitioned by status code, method and HTTP path.
    # TYPE chi_requests_total counter
    chi_requests_total{code="OK",method="GET",path="/metrics",service="serviceName"} 1
    chi_requests_total{code="OK",method="GET",path="/ok",service="serviceName"} 2

## Pattern Middleware Usage

Take a look at the [example](./pattern_example/main.go).

## What do you get

An endpoint with the following information (stripped output):

    # HELP chi_pattern_request_duration_milliseconds How long it took to process the request, partitioned by status code, method and HTTP path (with patterns).
    # TYPE chi_pattern_request_duration_milliseconds histogram
    chi_pattern_request_duration_milliseconds_bucket{code="OK",method="GET",path="/metrics",service="test_service",le="300"} 1
    chi_pattern_request_duration_milliseconds_bucket{code="OK",method="GET",path="/metrics",service="test_service",le="1200"} 1
    chi_pattern_request_duration_milliseconds_bucket{code="OK",method="GET",path="/metrics",service="test_service",le="5000"} 1
    chi_pattern_request_duration_milliseconds_bucket{code="OK",method="GET",path="/metrics",service="test_service",le="+Inf"} 1
    chi_pattern_request_duration_milliseconds_sum{code="OK",method="GET",path="/metrics",service="test_service"} 0.975926
    chi_pattern_request_duration_milliseconds_count{code="OK",method="GET",path="/metrics",service="test_service"} 1
    chi_pattern_request_duration_milliseconds_bucket{code="OK",method="GET",path="/users/{firstName}",service="test_service",le="300"} 0
    chi_pattern_request_duration_milliseconds_bucket{code="OK",method="GET",path="/users/{firstName}",service="test_service",le="1200"} 0
    chi_pattern_request_duration_milliseconds_bucket{code="OK",method="GET",path="/users/{firstName}",service="test_service",le="5000"} 2
    chi_pattern_request_duration_milliseconds_bucket{code="OK",method="GET",path="/users/{firstName}",service="test_service",le="+Inf"} 2
    chi_pattern_request_duration_milliseconds_sum{code="OK",method="GET",path="/users/{firstName}",service="test_service"} 4755.052755
    chi_pattern_request_duration_milliseconds_count{code="OK",method="GET",path="/users/{firstName}",service="test_service"} 2
    # HELP chi_pattern_requests_total How many HTTP requests processed, partitioned by status code, method and HTTP path (with patterns).
    # TYPE chi_pattern_requests_total counter
    chi_pattern_requests_total{code="OK",method="GET",path="/metrics",service="test_service"} 1
    chi_pattern_requests_total{code="OK",method="GET",path="/users/{firstName}",service="test_service"} 2


# Fork Information !!!

  This project was forked from edjumacator/chi-prometheus that
  had been forked from 766b with the intention of adding pattern matching to the logger.
  [Original Project Here](https://github.com/766b/chi-prometheus). This fork adds the
  possibility to register chi middleware handler to non-default prometheus registerer.
