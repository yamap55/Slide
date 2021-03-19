<style type="text/css">
  .reveal h1,
  .reveal h2,
  .reveal h3,
  .reveal h4,
  .reveal h5,
  .reveal h6 {
    text-transform: none;
  }
</style>

# PostgreSQLのデフォルトLOCALEの話

### yamap55

---

## アジェンダ

- 再現デモ
- 解決編
- まとめ
- 蛇足

---

## 再現デモ

--

## 起動

```
docker run -d --name postgres_1 postgres:11.5
docker exec -it postgres_1 psql -U postgres
```

--

## SQL

```
create table hoge ( id int, value varchar(10));
insert into hoge values
(1, 'あ'),
(2, 'あ（ほげ）'),
(3, 'い'),
(4, 'い（ふが）')
;
select * from hoge order by value;
```

--

## 結果

```
postgres=# select * from hoge order by value;
 id |   value    
----+------------
  1 | あ
  3 | い
  2 | あ（ほげ）
  4 | い（ふが）
(4 rows)
```

--

## LOCALEの確認

```
postgres=# SHOW LC_COLLATE;
 lc_collate 
------------
 en_US.utf8
(1 row)
```

--

## LC_COLLATE？

> LC_COLLATE	文字列の並び換え順

https://www.postgresql.jp/document/12/html/locale.html

---

## 解決編

--

## Dockerfile

```
FROM postgres:11.5
RUN localedef -i ja_JP -c -f UTF-8 -A /usr/share/locale/locale.alias ja_JP.UTF-8
ENV TZ=Asia/Tokyo
ENV LANG=ja_JP.UTF-8
ENV LANGUAGE=ja_JP:ja
ENV LC_ALL=ja_JP.UTF-8
```

--

## 起動

```
docker build . -t postgres_i
docker run -d --name postgres_2 postgres_i
docker exec -it postgres_2 psql -U postgres
```


--

## SQL

```
create table hoge ( id int, value varchar(10));
insert into hoge values
(1, 'あ'),
(2, 'あ（ほげ）'),
(3, 'い'),
(4, 'い（ふが）')
;
select * from hoge order by value;
```

--

## 結果

```
postgres=# select * from hoge order by value;
 id |   value    
----+------------
  1 | あ
  2 | あ（ほげ）
  3 | い
  4 | い（ふが）
(4 行)
```

--

## LOCALEの確認

```
postgres=# SHOW LC_COLLATE;
 lc_collate  
-------------
 ja_JP.UTF-8
(1 行)
```

---

## まとめ

--

- ちょっと使うだけでもしっかり設定しよう
- 日本という環境は不利
- 詳細はblogに書いた
  - https://yamap55.hatenablog.com/entry/2021/03/13/145223

---

## 蛇足

--

## MySQLの場合

--

## 起動

```
docker run --name mysql_1 -e MYSQL_ROOT_PASSWORD=mysql -d mysql
docker exec -it mysql_1 mysql -u root -p -h 127.0.0.1 -D mysql -pmysql
```

--

## SQL

```
mysql> create table hoge ( id int, value varchar(10));
Query OK, 0 rows affected (0.04 sec)

mysql> insert into hoge values
    -> (1, ''),
    -> (2, ''),
    -> (3, ''),
    -> (4, '')
    -> ;
Query OK, 4 rows affected (0.01 sec)
Records: 4  Duplicates: 0  Warnings: 0
```

※日本語が入力できない

--

## 結果

```
mysql> select * from hoge;
+------+-------+
| id   | value |
+------+-------+
|    1 |       |
|    2 |       |
|    3 |       |
|    4 |       |
+------+-------+
4 rows in set (0.00 sec)
```

--

## 確認1

```
mysql> status
--------------
mysql  Ver 8.0.23 for Linux on x86_64 (MySQL Community Server - GPL)
（略）
Server characterset:	utf8mb4
Db     characterset:	utf8mb4
Client characterset:	latin1
Conn.  characterset:	latin1
```

--

## 確認2

```
mysql> SHOW VARIABLES LIKE "char%";
+--------------------------+--------------------------------+
| Variable_name            | Value                          |
+--------------------------+--------------------------------+
| character_set_client     | latin1                         |
| character_set_connection | latin1                         |
| character_set_database   | utf8mb4                        |
| character_set_filesystem | binary                         |
| character_set_results    | latin1                         |
| character_set_server     | utf8mb4                        |
| character_set_system     | utf8                           |
| character_sets_dir       | /usr/share/mysql-8.0/charsets/ |
+--------------------------+--------------------------------+
8 rows in set (0.01 sec)
```

--

## クライアント側で変更できるらしい

- 接続前
```
docker exec -it mysql_1 mysql -u root -p -h 127.0.0.1 -D mysql -pmysql --default-character-set=utf8mb4
```

- 接続後
```
SET character_set_client = utf8mb4;
SET character_set_results = utf8mb4;
```

--

## 再度確認1

```
mysql> status
--------------
（略）
Server characterset:	utf8mb4
Db     characterset:	utf8mb4
Client characterset:	utf8mb4
Conn.  characterset:	utf8mb4
```

--

## 再度確認2

```
mysql> SHOW VARIABLES LIKE "char%";
+--------------------------+--------------------------------+
| Variable_name            | Value                          |
+--------------------------+--------------------------------+
| character_set_client     | utf8mb4                        |
| character_set_connection | utf8mb4                        |
| character_set_database   | utf8mb4                        |
| character_set_filesystem | binary                         |
| character_set_results    | utf8mb4                        |
| character_set_server     | utf8mb4                        |
| character_set_system     | utf8                           |
| character_sets_dir       | /usr/share/mysql-8.0/charsets/ |
+--------------------------+--------------------------------+
8 rows in set (0.00 sec)
```

--

## 結論

- だめでした
- サーバ側の設定を変更する必要があり（知ってた）
- [DockerのMySQLコンテナを日本語対応させる - Qiita](https://qiita.com/zongxiaojie/items/6b593ec4ce5e85bb342c)
  - 試してない

---

## ご清聴ありがとうございました
