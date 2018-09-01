FROM golang:1.10.3-alpine3.8

MAINTAINER Igor Semenyuk <igor.semenyuk@rolique.io>

RUN apk update && apk upgrade \
	&& apk add --no-cache ca-certificates \
	bash \
	git

COPY ./app/aws/credentials /root/.aws/credentials

COPY ./app $GOPATH/src/zipper

WORKDIR $GOPATH/src/zipper

# Install go package manager - dep.
RUN go get -d -u github.com/golang/dep && \
    cd $(go env GOPATH)/src/github.com/golang/dep && \
    DEP_LATEST=$(git describe --abbrev=0 --tags) && \
    git checkout $DEP_LATEST && \
    go install -ldflags="-X main.version=$DEP_LATEST" ./cmd/dep

# Install all dependencies
RUN dep ensure

CMD ["go", "run", "main.go"]
