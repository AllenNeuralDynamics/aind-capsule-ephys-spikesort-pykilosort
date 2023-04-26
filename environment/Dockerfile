# hash:sha256:74669169691831806c4fe44602cfacaae2a7c0f25db1ef06cfa9ab1af75fa9c0
FROM registry.codeocean.allenneuraldynamics.org/codeocean/pykilosort-base:latest

ARG DEBIAN_FRONTEND=noninteractive

ARG GIT_ASKPASS
ARG GIT_ACCESS_TOKEN
COPY git-askpass /

RUN pip install -U --no-cache-dir \
    aind-data-schema==0.13.11

COPY postInstall /
RUN /postInstall
