---
created: 2024-04-01T23:04
updated: 2024-04-02T23:11
---
- Java를 사용하는 어플리케이션에 mysql의 연결을 쉽게 하기 위해 개발됨
- JDBC type 4 driver이며, JDBC 4.2 specification을 구현함

- mysql connector-j를 사용해서 커넥션을 얻고, 구문을 실행하여 5번째 컬럼의 문자열 결과를 얻어오는 코드는 아래와 같음
```kotlin
DriverManager.getConnection("jdbc:mysql://localhost:3306/dreamStore","root","tjdgh123").use {conn ->  
    conn.createStatement().use { statment ->  
        val resultSet = statment.executeQuery("select * from product")  
        while(resultSet.next()){  
            println(resultSet.getString(5))  
        }  
    }  
}
```
- Connection을 한번 생성하면 데이터베이스에서 메타데이터를 가져오기 위한, Statement객체와 PrepareStatement객체를 생성하는데 사용 가능함