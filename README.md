# Prometheus fluent-bit monitoring

## Functionality

Bring up the containers by running,

    docker-compose up

To bring down and clean up the containers run,

    docker-compose down

## UI   

| Function       | URL                                              | Username  | Password |
|----------------|--------------------------------------------------|-----------|----------|
| Splunk UI      | [http://localhost:8000/](http://localhost:8000/) | admin     | admin    |

## Composition

This docker-compose image uses,

 - [A public, official splunk enterprise image](https://hub.docker.com/r/splunk/splunk/)
 - [A public, official fluentbit image](https://hub.docker.com/r/fluent/fluent-bit/)


## Shell

For a shell on the containers, run the commands below.

    ./script/shell-splunk.sh
    ./script/shell-fluentbit.sh

## Testing

The HEC port is exposed in the `docker-compose.yml` file. This opens the HEC on localhost:8088.

To see it in action, run the cURL command,

```
curl -u 'x:3e6ffd12-0f69-46bb-ad0d-71cffb661a0d' -X POST -d'
{
    "event": {
        "event_key1": "value1",
        "event_key1": "value1"
    },
    "fields": {
        "field_key1": "value1",
        "field_key1": "value1"
    }
}' http://localhost:8088/services/collector/event
```

If the interface is up and running, The expected response is,

```
{"text":"Success","code":0}
```

