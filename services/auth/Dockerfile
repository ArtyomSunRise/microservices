FROM golang:1.22-alpine3.19 AS build

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY ./ ./

RUN CGO_ENABLED=0 GOOS=linux go build -o /bin/main cmd/auth.go

FROM scratch AS final

WORKDIR /

COPY --from=build /bin/main /main

EXPOSE 8081

ENTRYPOINT ["/main"]