---
date: 2024-06-12 15:29:40
updatedAt: 2024-06-12 15:29:50
tags:
  - Java
  - Time-Zone
categories:
  - JVM
---
```java
private static synchronized TimeZone setDefaultZone() {  
    TimeZone tz;  
    // get the time zone ID from the system properties  
    Properties props = GetPropertyAction.privilegedGetProperties();  
    String zoneID = props.getProperty("user.timezone");  
  
    // if the time zone ID is not set (yet), perform the  
    // platform to Java time zone ID mapping.    if (zoneID == null || zoneID.isEmpty()) {  
        String javaHome = StaticProperty.javaHome();  
        try {  
            zoneID = getSystemTimeZoneID(javaHome);  
            if (zoneID == null) {  
                zoneID = GMT_ID;  
            }  
        } catch (NullPointerException e) {  
            zoneID = GMT_ID;  
        }  
    }  
  
    // Get the time zone for zoneID. But not fall back to  
    // "GMT" here.    tz = getTimeZone(zoneID, false);  
  
    if (tz == null) {  
        // If the given zone ID is unknown in Java, try to  
        // get the GMT-offset-based time zone ID,        // a.k.a. custom time zone ID (e.g., "GMT-08:00").        String gmtOffsetID = getSystemGMTOffsetID();  
        if (gmtOffsetID != null) {  
            zoneID = gmtOffsetID;  
        }  
        tz = getTimeZone(zoneID, true);  
    }  
    assert tz != null;  
  
    final String id = zoneID;  
    props.setProperty("user.timezone", id);  
  
    defaultTimeZone = tz;  
    return tz;  
}
```