# hash:sha256:56badfa0669faf4da373fa8861558666738a055586831e700acd9d7234b4cfdf
FROM registry.codeocean.allenneuraldynamics.org/codeocean/pykilosort-base:1.4.3

ARG DEBIAN_FRONTEND=noninteractive

ARG GIT_ASKPASS
ARG GIT_ACCESS_TOKEN
COPY git-askpass /

RUN pip install -U --no-cache-dir \
    aind-data-schema==0.13.54

COPY postInstall /
RUN /postInstall
