implementation("com.github.gavlyukovskiy:p6spy-spring-boot-starter:1.8.0")

database-platform: com.tpirates.conf.CustomDialect

decorator:
  datasource:
    p6spy:
      enable-logging: true

#Database 
#Library 
#쿼리
#쿼리보는도구 
#argent 