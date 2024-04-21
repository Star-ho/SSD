---
date: 2023-09-20T16:40:11
updatedAt: 2024-04-21 18:34:36+2420
tags: 
---
implementation("com.github.gavlyukovskiy:p6spy-spring-boot-starter:1.8.0")

database-platform: com.tpirates.conf.CustomDialect

decorator:
  datasource:
    p6spy:
      enable-logging: true

#Database 
#Library 
#쿼리보는도구 