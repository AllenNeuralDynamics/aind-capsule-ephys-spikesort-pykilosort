FROM spikeinterface/pykilosort-base:1.4.3.1

ARG DEBIAN_FRONTEND=noninteractive

RUN pip install -U --no-cache-dir \
    aind-data-schema==0.15.25

COPY postInstall /
RUN /postInstall
