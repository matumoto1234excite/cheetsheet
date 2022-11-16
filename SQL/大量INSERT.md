```sql
DROP PROCEDURE IF EXISTS insert_loop;
DELIMITER //
CREATE PROCEDURE insert_loop(IN cnt INT)
BEGIN
	DECLARE i INT DEFAULT 0;
	WHILE i < cnt DO
		SET cnt = cnt + 1;
		SET @user_id := UUID();
		
		INSERT
			INTO
				users(@user_id)
			VALUES
				(@user_id);

	END WHILE;
WHILE
//

DELIMITER ;

CALL insert_loop(1000);
```
 まあほんとはこういう感じで手続き的に書くのは良くないんだけど、ダミーデータを大量にINSERTするとかの目的であれば良さそうな気はする

あとはCROSS JOINとかで大量にINSERTする方法もあるらしい