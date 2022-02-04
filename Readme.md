* Swagger Link: http://localhost:8080/swagger-ui.html
* How to run:
  * mvn clean install
  * java -jar target/SampleQueue-1.0-SNAPSHOT.jar


Sample queue consumer register payload:
```
{
"callBackURL": "http://localhost:8080/queue/api/v1/debug/",
"consumerName": "string-consumer-2",
"queueName": "string-queue"
}
```


Sample payload for producer push:
```
{
  "payload": {
    "one": "yes",
    "two": false
  },
  "producerId": "string-producer",
  "queueName": "string-queue"
}
```

* There is a debug consumer exposed in the form of an APi with the functionality to switch between happy and non-happy code flow to test consumer side failures in terms of the queue offset management.
* Currently an in-memory MongoDB is used as a data store.
* And to handle race conditions on the offset number, currently findAndModify is used to leverage, but ideally to avoid slow performance, a cache based solution would be used.
* Some extensions are commented out in the request/model classes such as TTL, masking, etc which could be added later.
* To handle extension from consumer to consumer group thought, offset number would then be generated based on the partition number, and that would be just an extension.
* To make the system multi tenant, effort needs to be put into as how can we shard/club requests from multiple tenants.
