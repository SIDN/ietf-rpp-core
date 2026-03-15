FROM ghcr.io/ietf-tools/xml2rfc-base:latest

# Install golang and mmark

RUN apt-get -y update && apt-get -y install golang-go nano git && apt-get -y clean && \
    git clone https://github.com/mmarkdown/mmark.git && \
    cd mmark && go get && go build && mv mmark /usr/bin/

# Specify the working directory when a container is started
WORKDIR /workspace/draft-kowalik-rpp-data-objects