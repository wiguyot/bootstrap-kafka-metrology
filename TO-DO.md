1) Certains indicateurs ne sont pas reproduits d'un lancement sur l'autre du coup les dashboards préparés ne sont pas toujours opérationnels
2) ré-intégrer : 
 

```yaml
from(bucket: "kafka_metrics")
  |> range(start: v.timeRangeStart, stop: v.timeRangeStop)
  |> filter(fn: (r) => r["_measurement"] == "kafka_bytes_out" or r["_measurement"] == "kafka_bytes_in")
  |> derivative(unit: 1s, nonNegative: false)
  |> map(fn: (r) => ({
      r with
      _value: if r["_measurement"] == "kafka_bytes_out" then -1.0 * r._value else r._value
  }))
  |> yield(name: "signed_derivative")
  ```
  