---
title: Load Testing Improper Instantiation
description: 

author: dragon119
manager: christb

pnp.series.title: Optimize Performance
---
# Load Testing Improper Instantiation
[!INCLUDE [header](../../_includes/header.md)]

This document summarizes the configuration we used to perform load testing for the Improper Instantiation antipattern. You should also read about our [general approach][general approach] to deployment and load testing.

## Deployment

 Option             | Value  
------------------- | -------------
Compute             | Cloud Service
VM Size             | Large
Instance Count      | 1

## Test Configuration

The load test project included four web tests, each invoking an HTTP `GET` operation.

The URLs used were:

- http://yourservice.cloudapp.net/api/newhttpclientinstanceperrequest/{ProductID}
- http://yourservice.cloudapp.net/api/singlehttpclientinstance/{ProductID}
- http://yourservice.cloudapp.net/api/newserviceinstanceperrequest/{ProductID}
- http://yourservice.cloudapp.net/api/singleserviceinstance/{ProductID}

Replace *yourservice* with the name of your cloud service, and
replace *{ProductID}* with an product ID generated using the *Generate Random
Integer* plugin.

The project also included four load tests, one for each web test. All load tests were
run against a single deployment but at different times, using the following parameters:

Parameter           | Value
------------------- | ------------:
Initial User Count  | 1
Maximum User Count  | 1000
Step Duration       | 60s
Step Ramp Time      | 0s
Step User Count     | 100
Test Duration       | 10 minutes
Test Warm Up        | 30 seconds

The load test for the http://yourservice.cloudapp.net/api/newhttpclientinstanceperrequest/{ProductID} web test generated the following results:

![Load-test results][LoadTest1]

The load test for the http://yourservice.cloudapp.net/api/singlehttpclientinstance/{ProductID} web test generated the following results:

![Load-test results][LoadTest2]

The load test for the http://yourservice.cloudapp.net/api/newserviceinstanceperrequest/{ProductID web test generated the following results:

![Load-test results][LoadTest3]

The load test for the http://yourservice.cloudapp.net/api/singleserviceinstance/{ProductID} web test generated the following results:

![Load-test results][LoadTest4]

[general approach]: ../load-testing.md

[LoadTest1]: _images/HttpClientInstancePerRequest.jpg
[LoadTest2]: _images/SingleHttpClientInstance.jpg
[LoadTest3]: _images/ServiceInstancePerRequest.jpg
[LoadTest4]: _images/SingleServiceInstance.jpg