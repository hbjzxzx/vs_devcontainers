FROM haskell:9.0.2 AS builder

WORKDIR /build_hls
RUN git clone https://github.com/haskell/haskell-language-server.git hls

WORKDIR /build_hls/hls
RUN stack build --stack-yaml=stack-lts19.yaml
RUN stack install --local-bin-path=outputs --stack-yaml=stack-lts19.yaml
# RUN find . -maxdepth 1 -not -name ".stack-work" -not -name "." | xargs rm -rf

FROM haskell:9.0.2
COPY --from=builder /root/.stack /root/.stack
COPY --from=builder /build_hls/hls/outputs/* /usr/local/bin/
COPY --from=builder /build_hls/hls/.stack-work /build_hls/hls/.stack-work