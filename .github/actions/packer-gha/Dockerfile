#FROM hashicorp/packer:light
##FROM ubuntu:latest
#
#COPY "entrypoint.sh" "/entrypoint.sh"
#COPY "gha-base-ami" "/gha-base-ami"
#
#ENTRYPOINT ["/entrypoint.sh"]
#

FROM ubuntu:latest

RUN apt-get update && apt-get install -y \
  unzip \
  git \
  bash \
  wget \
  openssl
## Env setup
#ENV PACKER_VERSION=1.7.4 \
#    PACKER_OSNAME=linux \
#    PACKER_OSARCH=amd64 \
#    PACKER_DEST=/usr/local/sbin \
#    AWS_REGION=us-east-1
#
## Packer path setup
##ENV PACKER_ZIPFILE=packer_${PACKER_VERSION}_linux_amd64.zip
#ENV PACKER_ZIPFILE=https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip
#
## Install packer in path
#ADD https://releases.hashicorp.com/packer/${PACKER_VERSION}/${PACKER_ZIPFILE} ${PACKER_DEST}/
#RUN unzip ${PACKER_DEST}/${PACKER_ZIPFILE} -d ${PACKER_DEST} && \
#    rm -rf ${PACKER_DEST}/${PACKER_ZIPFILE}
#
#COPY "entrypoint.sh" "/entrypoint.sh"
#COPY "gha-base-ami" "/gha-base-ami"
#
#ENTRYPOINT ["/bin/bash","/entrypoint.sh"]

ENV PACKER_VERSION=1.7.4
ENV PACKER_SHA256SUM=3660064a56a174a6da5c37ee6b36107098c6b37e35cc84feb2f7f7519081b1b0

#RUN apk add --update git bash wget openssl

ADD https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip ./
ADD https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_SHA256SUMS ./

RUN sed -i '/.*linux_amd64.zip/!d' packer_${PACKER_VERSION}_SHA256SUMS
RUN sha256sum -cs packer_${PACKER_VERSION}_SHA256SUMS
RUN unzip packer_${PACKER_VERSION}_linux_amd64.zip -d /bin
RUN rm -f packer_${PACKER_VERSION}_linux_amd64.zip

COPY "entrypoint.sh" "/entrypoint.sh"
COPY "gha-base-ami" "/gha-base-ami"

ENTRYPOINT ["/bin/bash","/entrypoint.sh"]
