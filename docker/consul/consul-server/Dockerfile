# The container starts a consul-server

FROM warmfusion/consul-base:0.5
MAINTAINER Toby Jackson <toby@warmfusion.co.uk>

ADD ./config /config/
ADD https://dl.bintray.com/mitchellh/consul/0.5.2_web_ui.zip /tmp/webui.zip
RUN cd /tmp && unzip webui.zip && mv dist /ui && rm webui.zip

RUN mkdir /var/consul


ENTRYPOINT ["/bin/consul", "agent", "-server", "-config-dir=/config"]