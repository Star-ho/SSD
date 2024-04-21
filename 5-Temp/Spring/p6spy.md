---
date: 2024-03-31T22:41:00
updatedAt: 2024-04-21 18:32:05+2980
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