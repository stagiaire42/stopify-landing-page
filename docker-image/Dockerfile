FROM alpine:3.13 AS alpine

#
# Hugo
#
FROM alpine AS hugo
ADD _files/ /files
RUN chmod a+x /files/bin/*
ARG HUGO_VERSION
ENV HUGO_VERSION=${HUGO_VERSION}
ARG TARGETPLATFORM
ADD _script/hugo.sh hugo.sh
RUN sh hugo.sh

#
# Final stage
#
FROM alpine
ARG HUGO_VERSION
ENV HUGO_VERSION=${HUGO_VERSION}
ENV HUGO_BIND="0.0.0.0" \
    HUGO_DESTINATION="public" \
    HUGO_ENV="DEV" \
    HOME="/tmp"
COPY --from=hugo /files /
RUN apk --no-cache add busybox-suid bash bash-completion ca-certificates tzdata make \
 && find /tmp -mindepth 1 -maxdepth 1 | xargs rm -rf \
 && mkdir -p /src /target \
 && chmod a+w /src /target
EXPOSE 1313
WORKDIR /src
ENTRYPOINT ["hugo"]
