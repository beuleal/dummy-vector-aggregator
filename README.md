# Dummy Vector Aggregator

This Vector receives the data from Vector "Agent" and forwards to Loki

## Sources

Documentation: https://vector.dev/docs/reference/configuration/sources/

As the name suggest, the sources are "from where Vector" will collect the logs.

In our example, we are using `docker_logs` as it will collect the logs from dockerd. In aggregator, we are using `vector` opening a port to receive logs from vector agent.

## Transform

Documentation: https://vector.dev/docs/reference/configuration/transforms/

The best way to test the transformations is to copy one event as is and paste in a sample file, like `sample.log`.

Example:

```
{"container_created_at":"2024-07-16T22:55:05.012984341Z","container_id":"754e39cfd8ece46a36bbc5f652281a0647e7fa5b082158f297eae957316f336e","container_name":"dummy-python-api","host":"a7c35ce3166a","image":"dummy-python-api","label":{"com.docker.compose.config-hash":"582576e4cb9792741561a4be355471967992cbd13360ef177ecbf19a81be72aa","com.docker.compose.container-number":"1","com.docker.compose.depends_on":"","com.docker.compose.image":"sha256:22a99e78f72a7b6ae155772c966f7b5bd1070c7b81b89420e39745d005578997","com.docker.compose.oneoff":"False","com.docker.compose.project":"dummy-python-api","com.docker.compose.project.config_files":"/Users/brenno/Personal Workspace/dummy-python-api/docker-compose.yaml","com.docker.compose.project.working_dir":"/Users/brenno/Personal Workspace/dummy-python-api","com.docker.compose.replace":"f16cf535f72880290b55f192c9e4c7e12e6d07fd6a98c0b221097d3dbe2a749f","com.docker.compose.service":"dummy-python-api","com.docker.compose.version":"2.24.5"},"message":"{\"written_at\": \"2024-07-18T20:04:06.259Z\", \"written_ts\": 1721333046259214000, \"type\": \"request\", \"correlation_id\": \"e32111b4-4540-11ef-808f-0242ac120002\", \"remote_user\": \"-\", \"request\": \"/api/resource\", \"referer\": \"-\", \"x_forwarded_for\": \"-\", \"protocol\": \"HTTP/1.1\", \"method\": \"GET\", \"remote_ip\": \"192.168.65.1\", \"request_size_b\": -1, \"remote_host\": \"192.168.65.1\", \"remote_port\": 51329, \"request_received_at\": \"2024-07-18T20:04:06.258Z\", \"response_time_ms\": 0, \"response_status\": 401, \"response_size_b\": 52, \"response_content_type\": \"application/json\", \"response_sent_at\": \"2024-07-18T20:04:06.259Z\"}","source_type":"docker_logs","stream":"stdout"}
```

Then run a `vector vrl --input sample.log` - Vector Remap Language. If you are using docker to run vector, the input should be the container path, example `vector vrl --input /etc/vector/sample.log`.

## Sinks

Documentation: https://vector.dev/docs/reference/configuration/sinks/

As the name suggest, the sinks are the target where Vector needs to ship the log.

In our example, we are using `console` (stdout) and also Grafana Loki.
