FROM centos:7

RUN yum update -y && yum install -y wget && wget https://github.com/prometheus/prometheus/releases/download/v2.29.1/prometheus-2.29.1.linux-amd64.tar.gz

RUN tar -xzvf prometheus-2.29.1.linux-amd64.tar.gz -C /opt && mv /opt/prometheus-2.29.1.linux-amd64 /opt/prometheus

RUN groupadd -r prometheus && useradd -g prometheus -s /bin/bash -c "Prometheus user" prometheus && chown -R prometheus:prometheus /opt/prometheus

RUN rm -rf /opt/prometheus/prometheus.yml

COPY ./prometheus.yml /opt/prometheus/prometheus.yml

RUN chown prometheus:prometheus /opt/prometheus/prometheus.yml && chmod 755 /opt/prometheus/prometheus.yml

EXPOSE 9090
VOLUME  [ "/opt/prometheus" ]
WORKDIR /opt/prometheus

USER prometheus

ENTRYPOINT ["./prometheus"]
CMD        ["--config.file=prometheus.yml"]
