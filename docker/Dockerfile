FROM alpine:latest
LABEL authors "Darknet Villain <supervillain@riseup.net>"

ENV HOME_DIR="/home/opentracker"
ENV OT_DATA="$HOME_DIR/data"

RUN mkdir -p "$HOME_DIR" "$OT_DATA" \
    && adduser -S -h "$HOME_DIR" opentracker \
    && chown -R opentracker:nobody "$HOME_DIR" \
    && chmod -R 700 "$OT_DATA"

COPY src /src

RUN apk --no-cache add build-base zlib-dev \
    && cd /src/libowfat \
    && make \
    && cd ../i2p.i2p-opentracker \
    && make \
    && cp opentracker "$OT_DATA" \
    && chown opentracker "$OT_DATA"/opentracker && chmod +x "$OT_DATA"/opentracker \
    && rm -rf /src && apk --purge del build-base zlib-dev  

EXPOSE 6969

VOLUME "$OT_DATA"
WORKDIR "$OT_DATA"
USER opentracker

CMD ./opentracker -i 0.0.0.0
