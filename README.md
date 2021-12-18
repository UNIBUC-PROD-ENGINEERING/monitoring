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

## Stop monitoring layer
`docker-compose down` 
