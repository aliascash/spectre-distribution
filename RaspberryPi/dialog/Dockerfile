FROM spectreproject/github-uploader:latest
MAINTAINER HLXEasy <hlxeasy@gmail.com>

ARG GITHUB_TOKEN=1234567
ARG SPECTRECOIN_RELEASE=latest
ARG SPECTRECOIN_REPOSITORY=spectrecoin-sh-rpc-ui
ARG REPLACE_EXISTING_ARCHIVE=''
#ENV GITHUB_TOKEN=${GITHUB_TOKEN}
ENV ARCHIVE=Dialog-1.3-20180621.tgz

RUN mkdir -p /filesToUpload/

# Unfortunately it is not possible to use parameters on "--from=...",
# so we need separate Dockerfiles
COPY --from=spectreproject/spectre-builder-raspi:latest /newDialog/  /filesToUpload/

RUN cd /filesToUpload \
 && tar czf ${ARCHIVE} . \
 && github-release upload \
        --user spectrecoin \
        --security-token "${GITHUB_TOKEN}" \
        --repo "${SPECTRECOIN_REPOSITORY}" \
        --tag "${SPECTRECOIN_RELEASE}" \
        --name "${ARCHIVE}" \
        --file "/filesToUpload/${ARCHIVE}" \
        ${REPLACE_EXISTING_ARCHIVE} \
 && rm -rf /filesToUpload/* \
 && export GITHUB_TOKEN=---
