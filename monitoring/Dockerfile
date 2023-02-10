FROM prom/blackbox-exporter:latest as exporter

FROM alpine:latest
RUN apk update && apk add libcap
COPY --from=exporter /bin/blackbox_exporter /bin/blackbox_exporter
COPY --from=exporter /etc/blackbox_exporter/config.yml /etc/blackbox_exporter/config.yml

RUN setcap cap_net_raw+ep /bin/blackbox_exporter && apk del libcap

EXPOSE 9115
ENTRYPOINT [ "/bin/blackbox_exporter" ]
CMD [ "-config.file=/etc/blackbox_exporter/config.yml" ]