implementation("com.github.gavlyukovskiy:p6spy-spring-boot-starter:1.8.0")

database-platform: com.tpirates.conf.CustomDialect

decorator:
  datasource:
    p6spy:
      enable-logging: true

한결부동산


java -javaagent:/run/tpirates/pinpoint/pinpoint-bootstrap-2.4.2.jar -Dpinpoint.applicationName=1412.test  -Dpinpoint.config=/run/tpirates/pinpoint/pinpoint-root.config -Dserver.port=8081  -Dfile.encoding=UTF-8  -cp $( cat /app/jib-classpath-file ) $( cat /app/jib-main-class-file )

java -Dserver.port=8081  -Dfile.encoding=UTF-8   -cp $( cat /app/jib-classpath-file ) $( cat /app/jib-main-class-file )