# based on line 230 of statefulset.yaml
FROM busybox:latest 

# the statefulset init container is supposed to change ownership of the /usr/share/opensearch/data directory: chown -R 1000:1000 /usr/share/opensearch/data
RUN chmod -R g+rwX /usr 