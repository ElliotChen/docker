## Reference
1. [Elastic Github](https://github.com/elastic)
2. [Elastic Docker Guide](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html)
3. [Kibana Docker Guide](https://www.elastic.co/guide/en/kibana/current/docker.html)
4. [Logstash Docker Guide](https://www.elastic.co/guide/en/logstash/current/docker.html)


## Filebeat


## Logback

### Maven

```
<dependency>
	<groupId>net.logstash.logback</groupId>
	<artifactId>logstash-logback-encoder</artifactId>
</dependency>
```

### logback.xml

#### Filebeat

```
<appender name="filestash" class="ch.qos.logback.core.FileAppender">
	<file>./logs/logstash/logstash_${date}.log</file>
	<encoder charset="UTF-8" class="net.logstash.logback.encoder.LogstashEncoder">
		<customFields>{"application":"16log"}</customFields>
	</encoder>
</appender>
```


#### tcp

```
<appender name="logstash" class="net.logstash.logback.appender.LogstashTcpSocketAppender">
	<destination>127.0.0.1:5000</destination>
	<encoder class="net.logstash.logback.encoder.LogstashEncoder">
		<customFields>{"application":"16log"}</customFields>
	</encoder>
</appender>
```

### Shell

```
./filebeat -e -c filebeat.yml
```