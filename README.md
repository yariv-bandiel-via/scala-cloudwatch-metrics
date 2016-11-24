# scala-cloudwatch-metrics

**Work in progress**

A wrapper for sending Cloudwatch metrics in Scala

Extracted from the [Grid Project](https://github.com/guardian/grid)

## Usage

```scala
import com.amazonaws.auth.AWSCredentials
import com.gu.cloudwatch.metrics.CloudWatchMetrics


class AppMetrics(stage: String, creds: AWSCredentials)  
  extends CloudWatchMetrics(stage, creds) {

  val barCounter = new CountMetric("Bar")
  val fooTimer = new TimeMetric("Foo") 

} 

import scala.concurrent.Future
import scala.concurrent.ExecutionContext.Implicits.global
import com.gu.cloudwatch.metrics.FutureSyntax._

class AppMetricsExamples(appMetrics: AppMetrics) {
  Future {
    //Do something
  }.incrementOnFailure(appMetrics.barCounter) { case _ => true }
}
```
