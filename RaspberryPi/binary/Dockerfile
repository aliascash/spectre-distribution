FROM spectreproject/github-uploader:latest

ARG GITHUB_TOKEN=1234567
ARG SPECTRECOIN_RELEASE=latest
ARG SPECTRECOIN_REPOSITORY=spectre
#ENV GITHUB_TOKEN=${GITHUB_TOKEN}
ENV ARCHIVE=Spectrecoin-${SPECTRECOIN_RELEASE}-RaspberryPi.tgz

RUN mkdir -p /filesToUpload/usr/local/bin

# Unfortunately it is not possible to use parameters on "--from=...",
# so we need separate Dockerfiles
COPY --from=spectreproject/spectre-raspi:latest /usr/local/bin/spectrecoin  /filesToUpload/usr/local/bin/
COPY --from=spectreproject/spectre-raspi:latest /usr/local/bin/spectrecoind /filesToUpload/usr/local/bin/

RUN cd /filesToUpload \
 && tar czf ${ARCHIVE} . \
 && github-release upload \
        --user spectrecoin \
        --security-token "${GITHUB_TOKEN}" \
        --repo "${SPECTRECOIN_REPOSITORY}" \
        --tag "${SPECTRECOIN_RELEASE}" \
        --name "${ARCHIVE}" \
        --file "/filesToUpload/${ARCHIVE}" \
 && rm -rf /filesToUpload/* \
 && export GITHUB_TOKEN=---
