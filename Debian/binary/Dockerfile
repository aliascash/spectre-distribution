FROM spectreproject/github-uploader:latest

ARG GITHUB_TOKEN=1234567
#ENV GITHUB_TOKEN=${GITHUB_TOKEN}
ENV ARCHIVE=spectrecoin-wallet-debian.tgz

RUN mkdir -p /filesToUpload/usr/local/bin

# Unfortunately it is not possible to use parameters on "--from=...",
# so we need separate Dockerfiles
COPY --from=spectreproject/spectre:latest /usr/local/bin/spectrecoin  /filesToUpload/usr/local/bin/
COPY --from=spectreproject/spectre:latest /usr/local/bin/spectrecoind /filesToUpload/usr/local/bin/

RUN cd /filesToUpload \
 && tar czf ${ARCHIVE} . \
 && github-release upload \
        --user HLXEasy \
        --security-token "${GITHUB_TOKEN}" \
        --repo spectre-distribution \
        --tag latest \
        --name "${ARCHIVE}" \
        --file "/filesToUpload/${ARCHIVE}" \
 && rm -rf /filesToUpload/* \
 && export GITHUB_TOKEN=---
