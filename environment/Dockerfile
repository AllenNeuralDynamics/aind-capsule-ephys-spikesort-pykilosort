# hash:sha256:3742ae802613fdd4ca25f4d73c751a700b6d298f430fbc28a21e4b9cd4fd72b5
FROM registry.codeocean.allenneuraldynamics.org/codeocean/pykilosort-base:1.4.3

ARG DEBIAN_FRONTEND=noninteractive

ARG GIT_ASKPASS
ARG GIT_ACCESS_TOKEN
COPY git-askpass /

RUN pip install -U --no-cache-dir \
    aind-data-schema==0.13.66

COPY postInstall /
RUN /postInstall
