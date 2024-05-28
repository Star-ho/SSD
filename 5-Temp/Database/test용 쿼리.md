---
date: 2024-05-28 22:35:46
updatedAt: 2024-05-28 22:35:52
---
### 데이터 삽입
```

drop procedure if exists insert_data;

DELIMITER //

CREATE PROCEDURE insert_data()
BEGIN
    DECLARE counter INT UNSIGNED DEFAULT 1;
    
    WHILE counter <= 100000 DO
        INSERT INTO t2 (i) VALUES (counter);
        SET counter = counter + 1;
    END WHILE;
END//

DELIMITER ;

CALL insert_data();
```