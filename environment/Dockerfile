# hash:sha256:836c17d3e8c9d09a44d75439defa7420306a63d6dfb70761d6ba1395fecf4619
FROM registry.codeocean.allenneuraldynamics.org/codeocean/pykilosort-base:1.4.3.1

ARG DEBIAN_FRONTEND=noninteractive

ARG GIT_ASKPASS
ARG GIT_ACCESS_TOKEN
COPY git-askpass /

RUN pip install -U --no-cache-dir \
    aind-data-schema==0.17.1

COPY postInstall /
RUN /postInstall
