FROM alpine:3.5

MAINTAINER Igor Semenyuk <igor.semenyuk@rolique.io>

COPY        ./app/aws/credentials /root/.aws/credentials

WORKDIR     /usr/local/bin
ADD         ./build/zipper .
RUN         apk add --update ca-certificates && \
            chmod +x /usr/local/bin/zipper && \
            rm -Rf /var/cache/apk/*

CMD         "./zipper"
