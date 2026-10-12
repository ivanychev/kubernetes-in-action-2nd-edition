# syntax=docker/dockerfile:1
FROM --platform=$BUILDPLATFORM golang:1.15.2-alpine AS build
ARG TARGETOS
ARG TARGETARCH
WORKDIR /src
COPY app/go.mod app/go.sum ./
RUN go mod download
COPY app/ ./
RUN CGO_ENABLED=0 GOOS=$TARGETOS GOARCH=$TARGETARCH go build -o /out/quiz-api .

FROM alpine
COPY --from=build /out/quiz-api /quiz-api
ENTRYPOINT ["/quiz-api"]
