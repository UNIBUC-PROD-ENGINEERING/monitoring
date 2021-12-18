## Start monitoring layer
* Start all the containers
  * `docker-compose up -d`

## Prometheus
* Check which targets is Prometheus monitoring:
  * http://localhost:9090/targets
* Plot metrics in Prometheus
  * Navigate to: http://localhost:9090
  * Invoke the application endpoints a couple of times so they start generating metrics:
    * http://localhost:8080/hello-world
    * http://localhost:8080/info
  * Wait 15s (default scrape interval)  
  * Paste `invocation_count_total{endpoint="hello"}` and choose Execute and Graph
  * Paste `invocation_duration_seconds_max{endpoint="info"}` and choose Execute and Graph


## Grafana
* Log in with `admin:admin` in Grafana UI
  * http://localhost:3000
* Add Prometheus datasource:
  * From Settings/Datasources or http://localhost:3000/datasources
  * Use as URL: http://prometheus:9090 
* Create a dashboard to plot invocation_count_total:
  * From the __+__ sign choose "Create -> Dashboard -> Add New Panel"
  * Select `Prometheus` as datasource for the panel, and paste `invocation_count_total{endpoint="hello"}`

## Alerting manager configuration
  * Configure Alert Manager notification channels in [prometheus-alert-manager.yml](labs/monitoring/prometheus/prometheus-alert-manager.yml)
    * Config example given for Gmail.

## Prometheus alerting rules and Alerting Manager
* Check the Prometheus alerting rules in prometheus UI
  * http://localhost:9090/alerts
* Check the Prometheus alerting rules yaml
  * [prometheus-alert-rules.yml](labs/monitoring/prometheus/prometheus-alert-rules.yml)
* Stop the hello world application and notice how in http://localhost:9090/alerts the **hello_world_service_down** alert enters PENDING and then FIRING.
* Navigate to Alert Manager UI to see firing alerts
  * http://localhost:9093/#/alerts 
  * Silence the firing **hello_world_service_down** alert for 1 hour
  
## Stop monitoring layer
`docker-compose down` 
