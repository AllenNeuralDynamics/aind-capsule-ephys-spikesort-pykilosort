# hash:sha256:3a679cfb5e222ee76dc8ff657a3069fd09c0e237973228e54d8dbe7b55909d03
FROM registry.codeocean.allenneuraldynamics.org/codeocean/pykilosort-base:1.4.3.1

ARG DEBIAN_FRONTEND=noninteractive

ARG GIT_ASKPASS
ARG GIT_ACCESS_TOKEN
COPY git-askpass /

RUN pip install -U --no-cache-dir \
    aind-data-schema==0.13.66

COPY postInstall /
RUN /postInstall
