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
  unzip
# Env setup
ENV PACKER_VERSION=1.7.4 \
    PACKER_OSNAME=linux \
    PACKER_OSARCH=amd64 \
    PACKER_DEST=/usr/local/sbin \
    AWS_REGION=us-east-1

# Packer path setup
#ENV PACKER_ZIPFILE=packer_${PACKER_VERSION}_linux_amd64.zip
ENV PACKER_ZIPFILE=https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip

# Install packer in path
ADD https://releases.hashicorp.com/packer/${PACKER_VERSION}/${PACKER_ZIPFILE} ${PACKER_DEST}/
RUN unzip ${PACKER_DEST}/${PACKER_ZIPFILE} -d ${PACKER_DEST} && \
    rm -rf ${PACKER_DEST}/${PACKER_ZIPFILE}

COPY "entrypoint.sh" "/entrypoint.sh"
COPY "gha-base-ami" "/gha-base-ami"

ENTRYPOINT ["/bin/bash","/entrypoint.sh"]
