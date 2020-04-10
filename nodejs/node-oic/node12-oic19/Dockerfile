FROM node:12.11.1-slim
MAINTAINER Okassov Marat <okasov.marat@gmail.com>

# Add oracle instantclient binaries
ADD *.zip ./

ENV LD_LIBRARY_PATH="/opt/oracle/instantclient"
ENV OCI_HOME="/opt/oracle/instantclient"
ENV OCI_LIB_DIR="/opt/oracle/instantclient"
ENV OCI_INCLUDE_DIR="/opt/oracle/instantclient/sdk/include"
ENV OCI_VERSION=19

# Install dependencies and extract binaries`
RUN apt-get update \
  && apt-get install -y unzip libaio1 musl-dev \
  && mkdir -p /opt/oracle \
  && unzip instantclient-*.zip -d /opt/oracle \
  && mv "${LD_LIBRARY_PATH}_19_3" $LD_LIBRARY_PATH \
  && ln -s /usr/lib/x86_64-linux-musl/libc.so /lib/libc.musl-x86_64.so.1 \
  && rm -f instantclient-*.zip \
  && apt-get remove -y unzip \
  && apt-get clean autoclean \
  && apt-get autoremove -y \
  && rm -rf /var/lib/{apt,dpkg,cache,log}/

#Create the necessary links and cache
RUN echo "${LD_LIBRARY_PATH}" | tee -a /etc/ld.so.conf.d/oracle_instant_client.conf && ldconfig

