# Configuration Server

This project is based on [Spring Cloud Config](https://cloud.spring.io/spring-cloud-config/) to centralize configuration files from each microservices.

All configuration files were stored at [configuration's repository](https://github.com/newzik/be-microservices-config)

## Getting Started

### Prerequisites

Connect configuration repository with credentials, open file application.yml for more detail

```
server:
  port: 8085
spring:
  application:
    name: config-server
  cloud:
    config:
      server:
        git:
          uri: https://github.com/newzik/be-microservices-config.git
          username: gh-backend-machine@newzik.com
          password: n<{PcMGyuYQe%4{d
```

### Running project

Run project via command line or IDE 

```
mvnw spring-boot:run
```

When server is started, the port number will be 8085. You can fetch configuration file from this server.

Exp: If you want to get configuration file of project authorization-service and profile is staging. The url will be 

```
GET http://localhost:8085/authorization-serice/staging
```

And response:

```
{
	"name": "authorization-service",
	"profiles": [
		"staging"
	],
	"label": null,
	"version": "2d01f098ce9e53add4814d7026833f66276d1b71",
	"state": null,
	"propertySources": [
		{
			"name": "https://github.com/newzik/be-microservices-config.git/authorization-service-staging.yml",
			"source": {
				"server.port": 8083,
				"server.use-forward-headers": false,
				"server.servlet.context-path": "/uaa",
				"spring.profiles": "staging",
				"spring.application.name": "auth-server",
				"spring.datasource.url": "jdbc:mysql://localhost:3306/oauth2?useSSL=false",
				"spring.datasource.username": "root",
				"spring.datasource.password": 12345,
				"spring.datasource.driver-class-name": "com.mysql.jdbc.Driver",
				"spring.datasource.tomcat.test-while-idle": true,
				"spring.datasource.tomcat.validation-query": "SELECT 1",
				"spring.datasource.initialization-mode": "never",
				"spring.datasource.platform": "mysql",
				"spring.jpa.properties.hibernate.dialect": "org.hibernate.dialect.MySQL5Dialect",
				"spring.jpa.hibernate.naming.physical-strategy": 						"org.springframework.boot.orm.jpa.hibernate.SpringPhysicalNamingStrategy",
				"spring.jpa.hibernate.ddl-auto": "validate",
				"spring.cloud.config.allow-override": true,
				"spring.cloud.config.override-none": true,
				"spring.liquibase.change-log": "classpath:db/liquibase/db-changelog.xml",
				"spring.zipkin.enabled": true,
				"spring.zipkin.base-url": "http://localhost:8087/",
				"spring.sleuth.sampler.probability": 1,
				"spring.sleuth.feign.enabled": true,
				"check-user-scopes": true,
				"logging.level.ROOT": "info",
				"logging.level.org.springframework.web": "info",
				"logging.level.com.enrico.microservices": "info",
				"eureka.instance.hostname": "localhost",
				"eureka.instance.port": 8081,
				"eureka.client.registerWithEureka": true,
				"eureka.client.fetchRegistry": true,
				"eureka.client.serviceUrl.defaultZone": 					"http://${eureka.instance.hostname}:${eureka.instance.port}/eureka/",
				"eureka.server.wait-time-in-ms-when-sync-empty": 3000
			}
		}
	]
}
```

### Override properties

Incase you want to override value of properties, you can update values from file application.yml of each microservices