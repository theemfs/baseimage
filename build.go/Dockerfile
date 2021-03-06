FROM golang:1.11-alpine

ENV CGO_ENABLED=0
ENV GOOS=linux
ENV GOARCH=amd64
ENV GOMETALINTER=2.0.11
ENV GOVERALLS=v0.0.2

RUN \
    apk add --no-cache --update tzdata git bash curl && \
    cp /usr/share/zoneinfo/America/Chicago /etc/localtime && \
    rm -rf /var/cache/apk/*

RUN \
    go version && \
    go get -u -v github.com/alecthomas/gometalinter && \
    cd /go/src/github.com/alecthomas/gometalinter && \
    git checkout v${GOMETALINTER} && \
    go install github.com/alecthomas/gometalinter && \
    gometalinter --install && \
    go get -u -v github.com/GoASTScanner/gas && \
    go get -u -v github.com/golang/dep/cmd/dep && \
    go get -u -v github.com/kardianos/govendor && \
    go get -u -v github.com/jteeuwen/go-bindata/... && \
    go get -u -v github.com/stretchr/testify && \
    go get -u -v github.com/vektra/mockery/.../

RUN \
    go get -u -v github.com/mattn/goveralls && \
    cd /go/src/github.com/mattn/goveralls && \
    git checkout $GOVERALLS && \
    go install github.com/mattn/goveralls

ADD coverage.sh /script/coverage.sh
ADD git-rev.sh /script/git-rev.sh

RUN chmod +x /script/coverage.sh /script/git-rev.sh
