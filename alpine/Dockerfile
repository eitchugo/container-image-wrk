# builder image
FROM alpine:3.14 as builder
WORKDIR /root
RUN apk add --update alpine-sdk perl lua5.1-dev luajit-dev openssl-dev
RUN wget -c https://github.com/wg/wrk/archive/refs/tags/4.1.0.tar.gz && tar -zpvxf 4.1.0.tar.gz
RUN cd wrk-4.1.0 && make WITH_LUAJIT=/usr WITH_OPENSSL=/usr

# runtime image
FROM alpine:3.14
LABEL maintainer="hugo.cisneiros@gmail.com"

ARG BUILD_DATE
LABEL org.label-schema.schema-version="1.0"
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.name="wrk"
LABEL org.label-schema.description="wrk http benchmarking tool"
LABEL org.label-schema.vcs-url="https://github.com/eitchugo/container-image-wrk"
LABEL org.label-schema.vendor="Hugo Cisneiros"

# dependencies for wrk and its scripting
RUN apk add --update lua5.1 luajit lua5.1-cjson lua5.1-rapidjson lua5.1-yaml \
    lua5.1-curl lua5.1-lpeg lua5.1-sqlite lua5.1-curl lua5.1-uuid
COPY --from=builder /root/wrk-4.1.0/wrk /usr/local/bin/

# run as a normal user please
RUN addgroup -S wrk
RUN adduser -S wrk -G wrk
USER wrk
ENV PATH="/home/wrk/bin:/home/wrk/.local/bin:/usr/local/bin:${PATH}"

# sample wrk scripts
COPY --from=builder /root/wrk-4.1.0/scripts /home/wrk/sample-scripts

WORKDIR /home/wrk
CMD ["wrk"]