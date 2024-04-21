---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 15:23:53+8670
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