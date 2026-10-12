# syntax=docker/dockerfile:1
FROM --platform=$BUILDPLATFORM golang:1.16 AS build
ARG TARGETOS
ARG TARGETARCH
WORKDIR /src
COPY app/go.mod app/go.sum ./
RUN go mod download
COPY app/ ./
RUN CGO_ENABLED=0 GOOS=$TARGETOS GOARCH=$TARGETARCH go build -o /out/static-http-server .

FROM alpine
COPY --from=build /out/static-http-server /server
ENTRYPOINT ["/server"]
