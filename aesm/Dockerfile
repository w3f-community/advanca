FROM ubuntu:18.04

ARG PSW_PKG_VERSION=2.9.101.2-bionic1
RUN apt-get update && apt-get install -y apt-utils
RUN apt-get install -y dkms gnupg2 apt-transport-https software-properties-common curl && \
    curl -fsSL  https://download.01.org/intel-sgx/sgx_repo/ubuntu/intel-sgx-deb.key | apt-key add - && \
    add-apt-repository "deb https://download.01.org/intel-sgx/sgx_repo/ubuntu bionic main" && \
    apt-get update && \
    apt-get install -y \
    	libsgx-launch=$PSW_PKG_VERSION \
	libsgx-aesm-epid-plugin=$PSW_PKG_VERSION \
	libsgx-aesm-pce-plugin=$PSW_PKG_VERSION \
	libsgx-pce-logic=1.6.100.2-bionic1 \
	libsgx-ae-le=$PSW_PKG_VERSION \
	libsgx-ae-epid=$PSW_PKG_VERSION \
	libsgx-aesm-launch-plugin=$PSW_PKG_VERSION \
	libsgx-aesm-launch-plugin=$PSW_PKG_VERSION \
	libsgx-enclave-common=$PSW_PKG_VERSION \
	libsgx-urts=$PSW_PKG_VERSION \
	libsgx-epid=$PSW_PKG_VERSION \
	libsgx-urts=$PSW_PKG_VERSION \
	libsgx-uae-service=$PSW_PKG_VERSION \
	libsgx-quote-ex=$PSW_PKG_VERSION \
	libsgx-urts=$PSW_PKG_VERSION \
	sgx-aesm-service=$PSW_PKG_VERSION

RUN mkdir -p /var/run/aesmd/ && chown -R aesmd:aesmd /var/run/aesmd/ && chmod 0755 /var/run/aesmd/

USER aesmd
WORKDIR /opt/intel/sgx-aesm-service/aesm

ENV LD_LIBRARY_PATH=/opt/intel/sgx-aesm-service/aesm

VOLUME /var/run/aesmd

CMD ./aesm_service --no-daemon
