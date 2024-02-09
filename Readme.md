## HOW TO AUTHENTICATE kibana (Set password based authentication)

Run

```
elasticsearch-reset-password -u kibana_system --auto
```

inside ES container once.
This will generate kibana_system user's password.
Now use this generated password in docker-compose.yml for kibana service like this:

```
kibana:
    image: docker.elastic.co/kibana/kibana:${STACK_VERSION}
    container_name: kibana
    volumes:
        - kibanadata:/usr/share/kibana/data
    environment:
        - ELASTICSEARCH_HOSTS="http://es01:${ES_PORT}"
        - ELASTICSEARCH_USERNAME=kibana_system
        - ELASTICSEARCH_PASSWORD=mnuuf6Ax2jRD7nSyB\*5A
        - xpack.security.enabled=true
    links: - es01
    ports: - ${KIBANA_PORT}:5601
        networks:
        - elastic
        depends_on:
        - es01
```

And restart kibana

```
docker-compose restart kibana
```
