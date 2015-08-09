# The container starts a consul-server

FROM warmfusion/consul-base:0.5
MAINTAINER Toby Jackson <toby@warmfusion.co.uk>

ADD ./config /config/
ADD https://dl.bintray.com/mitchellh/consul/0.5.2_web_ui.zip /tmp/webui.zip
RUN cd /tmp && unzip webui.zip && mv dist /ui && rm webui.zip

RUN mkdir /var/consul

# The consul-server docker runs on standard ports + 10,000
#   so it can run alongside the consul-agent
EXPOSE 8300 8301 8301/udp 8302 8302/udp 8400 8500 8600 8600/udp

ENTRYPOINT ["/bin/consul", "agent", "-server", "-config-dir=/config"]