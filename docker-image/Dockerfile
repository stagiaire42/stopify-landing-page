FROM alpine:3.13

ADD _script/hugo.sh hugo.sh
RUN sh hugo.sh && rm hugo.sh

ENV HOME="/tmp"
RUN apk --no-cache add bash bash-completion ca-certificates tzdata \
 && find /tmp -mindepth 1 -maxdepth 1 | xargs rm -rf \
 && mkdir -p /src /target \
 && chmod a+w /src /target

EXPOSE 1313

WORKDIR /src

ENTRYPOINT ["hugo"]
