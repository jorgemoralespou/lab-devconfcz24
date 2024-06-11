FROM golang:alpine as builder
RUN apk --update --no-cache add bash
WORKDIR /app
ADD . .
RUN go build -o app

FROM alpine as prod
LABEL org.opencontainers.image.source="https://github.com/jorgemoralespou/lab-devconfcz24"
USER 1001
WORKDIR /app
COPY --from=builder /app/app /app/app
EXPOSE 8080
CMD ["./app"]
