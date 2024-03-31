---
created: 2023-09-20T16:40:11
date: 2024-03-03T11:41
updated: 2024-03-31T22:43
---
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