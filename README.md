# livestub

[![Build Status](https://travis-ci.org/softwaremill/livestub.svg?branch=master)](https://travis-ci.org/softwaremill/livestub)
[![Docker Pulls](https://img.shields.io/docker/pulls/softwaremill/sttp.livestub.svg)](https://hub.docker.com/r/softwaremill/sttp.livestub/)
[![ImageLayers](https://images.microbadger.com/badges/image/softwaremill/sttp.livestub.svg)](https://microbadger.com/#/images/softwaremill/sttp.livestub)
[![Scala Steward badge](https://img.shields.io/badge/Scala_Steward-helping-brightgreen.svg?style=flat&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAQCAMAAAARSr4IAAAAVFBMVEUAAACHjojlOy5NWlrKzcYRKjGFjIbp293YycuLa3pYY2LSqql4f3pCUFTgSjNodYRmcXUsPD/NTTbjRS+2jomhgnzNc223cGvZS0HaSD0XLjbaSjElhIr+AAAAAXRSTlMAQObYZgAAAHlJREFUCNdNyosOwyAIhWHAQS1Vt7a77/3fcxxdmv0xwmckutAR1nkm4ggbyEcg/wWmlGLDAA3oL50xi6fk5ffZ3E2E3QfZDCcCN2YtbEWZt+Drc6u6rlqv7Uk0LdKqqr5rk2UCRXOk0vmQKGfc94nOJyQjouF9H/wCc9gECEYfONoAAAAASUVORK5CYII=)](https://scala-steward.org)

## Usage

### launch
 - **coursier**

    `coursier launch com.softwaremill.sttp.livestub:livestub-app_2.13:0.1.4-SNAPSHOT -- -p 8081`

- **docker**

    `docker run -p 8081:7070 softwaremill/sttp.livestub`

### stub
```
curl -X POST 'localhost:8081/__set' \
-d '{"when":{"method":"GET", "path":"animals/1/status"}, "then": {"statusCode":200, "body":{"status": "happy"} }}'
```

### invoke
```
curl 'localhost:8081/animals/1/status'
{"status":"happy"}
```

### swagger

Swagger is available under `/__admin/docs`

### advanced stubbing

Livestub supports wildcard http methods as well as wildcard path parameters.

wildcard method:
```
curl -X POST '172.17.0.1:7070/__set' \
-d '{"when":{"method":"*", "path":"dogs"}, "then": {"statusCode":200, "body":{"status": "OK"} }}'
```

wildcard path param: 
```
curl -X POST '172.17.0.1:7070/__set' \
-d '{"when":{"method":"GET", "path":"dogs/*/status"}, "then": {"statusCode":200, "body":{"status": "happy"} }}'
```

multiwildcard path param: (this one catches all routes which originate from `/dogs`)
```
curl -X POST '172.17.0.1:7070/__set' \
-d '{"when":{"method":"GET", "path":"dogs/**"}, "then": {"statusCode":200, "body":{"status": "cheerful"} }}'
```
