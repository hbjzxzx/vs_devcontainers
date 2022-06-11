FROM haskell:9.0.2 AS builder

WORKDIR /build_hls
RUN git clone https://github.com/haskell/haskell-language-server.git hls

WORKDIR /build_hls/hls
RUN stack build --stack-yaml=stack-lts19.yaml
RUN stack --local-bin-path outputs install --stack-yaml=stack-lts19.yaml

FROM haskell:9.0.2
COPY --from=builder /build_hls/hls/outputs/* /usr/bin/