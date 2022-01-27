# Spring actuator
## 서버의 모니터링 지표를 확인
- 통계, 서버의 세부상태, 데이터베이스의 연결
- spring actuator의 경우에는 자동설정 정보를 사용하여 정보를 반환함.

## Spring actuator의 추가
```
# gradle
implementation 'org.springframework.boot:spring-boot-starter-actuator'

# pom
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

## 기본 설정상태(application.properties)

### 서버 상태 세부정보 표시 설정
- 명령어
  - management.endpoint.health.show-details=(always, never, when_authorized)
- 설명
  - always의 경우에는 상태, ping, 디스크용량에 대한 상태까지 설정이 되어 있습니다.
  - http://localhost:8080/actuator/health 을 통해서 하기의 내용을 확인할 수 있습니다.
    - 또한, 위의 설명과 같이 자동설정 정보를 사용하는 만큼, 몽고디비 상태 및 버젼 정보등도 확인이 가능합니다.
- 궁금증
  - `components` 라고 하는 부분은 무엇인가?
```json
// always
{
  "status": "UP",
  "components": {
    "diskSpace": {
      "status": "UP",
      "details": {
        "total": 499963174912,
        "free": 362648858624,
        "threshold": 10485760,
        "exists": true
      }
    },
    "ping": {
      "status": "UP"
    }
  }
}
```

```json
// never, when_authorized
{
  "status": "UP"
}
```

### 애플리케이션 버젼 정보
- 명령어
  - info.project.version=@project.version@
  - info.java.version=@java.version@
  - info.spring.framwork.version=@spring-framework.version@
  - info.spring.data.version=@spring-data-bom.version@
- 설명
  - 프로젝트 정보, 자바버젼 정보, 스프링프레임워크 버젼 등을 알수 있습니다.
  - http://localhost:8080/actuator/info
- 궁금증
  - 왜 information 정보가 나오지 않을까?

  ### 모든 액추에이터 엔드포인트로 확인
  - 명령어
    - management.endpoints.web.exposure.include=*
      - auditevents, beans, caches, conditions, configprops, env, flyway, health, heapdump, httptrace, info, logfile, logger, metrics, mappings, shutdown, threaddump
  - 앤드포인트의 내역은 http://localhost:8080/actuator 로 들어가면, 확인할 수 있는 url 리스트가 표출된다.

```json

  "_links": {
    "self": {
      "href": "http://localhost:8080/actuator",
      "templated": false
    },
    "beans": {
      "href": "http://localhost:8080/actuator/beans",
      "templated": false
    },
    "caches-cache": {
      "href": "http://localhost:8080/actuator/caches/{cache}",
      "templated": true
    },
    "caches": {
      "href": "http://localhost:8080/actuator/caches",
      "templated": false
    },
    "health-path": {
      "href": "http://localhost:8080/actuator/health/{*path}",
      "templated": true
    },
    "health": {
      "href": "http://localhost:8080/actuator/health",
      "templated": false
    },
    "info": {
      "href": "http://localhost:8080/actuator/info",
      "templated": false
    },
    "conditions": {
      "href": "http://localhost:8080/actuator/conditions",
      "templated": false
    },
    "configprops-prefix": {
      "href": "http://localhost:8080/actuator/configprops/{prefix}",
      "templated": true
    },
    "configprops": {
      "href": "http://localhost:8080/actuator/configprops",
      "templated": false
    },
    "env": {
      "href": "http://localhost:8080/actuator/env",
      "templated": false
    },
    "env-toMatch": {
      "href": "http://localhost:8080/actuator/env/{toMatch}",
      "templated": true
    },
    "loggers": {
      "href": "http://localhost:8080/actuator/loggers",
      "templated": false
    },
    "loggers-name": {
      "href": "http://localhost:8080/actuator/loggers/{name}",
      "templated": true
    },
    "heapdump": {
      "href": "http://localhost:8080/actuator/heapdump",
      "templated": false
    },
    "threaddump": {
      "href": "http://localhost:8080/actuator/threaddump",
      "templated": false
    },
    "metrics-requiredMetricName": {
      "href": "http://localhost:8080/actuator/metrics/{requiredMetricName}",
      "templated": true
    },
    "metrics": {
      "href": "http://localhost:8080/actuator/metrics",
      "templated": false
    },
    "scheduledtasks": {
      "href": "http://localhost:8080/actuator/scheduledtasks",
      "templated": false
    },
    "mappings": {
      "href": "http://localhost:8080/actuator/mappings",
      "templated": false
    }
  }
}

```

### 관리 서비스의 경로를 수정하기
- management.endpoints.web.base-path=/manage