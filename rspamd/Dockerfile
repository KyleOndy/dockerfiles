ARG REGISTRY
FROM $REGISTRY/alpine:3.12
RUN apk add --no-cache \
    rspamd \
    rspamd-controller \
    rspamd-proxy
RUN echo -e 'filename = "/dev/stdout";' > /etc/rspamd/local.d/logging.inc
RUN echo -e 'local_addrs = [];' > /etc/rspamd/override.d/options.inc
COPY multimap.conf /etc/rspamd/local.d/multimap.conf
RUN mkdir /etc/rspamd/maps
COPY blacklist_domain.map /etc/rspamd/maps/
RUN sed -i 's@localhost:11334@*:11334@g' /etc/rspamd/worker-controller.conf
USER rspamd
WORKDIR /var/lib/rspamd
CMD ["rspamd", "--no-fork", "--pid", "/dev/null"]
