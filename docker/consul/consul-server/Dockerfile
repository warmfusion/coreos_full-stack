# The container starts a consul-server

FROM warmfusion/consul-base:0.5
MAINTAINER Toby Jackson <toby@warmfusion.co.uk>

ADD ./config /config/
ADD https://dl.bintray.com/mitchellh/consul/0.5.2_web_ui.zip /tmp/webui.zip
RUN cd /tmp && unzip webui.zip && mv dist /ui && rm webui.zip

RUN mkdir /var/consul

#The consul-server docker runs on standard ports + 10,000
# so it can run alongside the consul-agent
EXPOSE 18300 18301 18301/udp 18302 18302/udp 18400 18500 18600 18600/udp

ENTRYPOINT ["/bin/consul", "agent", "-server", "-config-dir=/config"]