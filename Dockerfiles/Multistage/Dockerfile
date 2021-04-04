FROM golang AS build

WORKDIR /app
ADD . /app
RUN go build -o meugo

FROM alpine

WORKDIR /apolo
#copiar do build/app/meugo e copiar para /app
COPY --from=build /app/meugo /apolo

ENTRYPOINT ./meugo