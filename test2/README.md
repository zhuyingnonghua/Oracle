# 实验二：用户管理 - 掌握管理角色、权根、用户的能力，并在用户之间共享对象
---
### 实验内容：
Oracle有一个开发者角色resource，可以创建表、过程、触发器等对象，但是不能创建视图。本训练要求：
- 在pdborcl插接式数据中创建一个新的本地角色con_res_view，该角色包含connect和resource角色，同时也包含CREATE VIEW权限，这样任何拥有con_res_view的用户就同时拥有这三种权限。
- 创建角色之后，再创建用户new_user，给用户分配表空间，设置限额为50M，授予con_res_view角色。
- 最后测试：用新用户new_user连接数据库、创建表，插入数据，创建视图，查询表和视图的数据。
## 实验步骤
- 第1步：以system登录到pdborcl，创建角色con_res_view和用户new_user，并授权和分配空间：
```sql
$ sqlplus system/123@pdborcl
SQL> CREATE ROLE con_res_views;
Role created.
SQL> GRANT connect,resource,CREATE VIEW TO con_res_views;
Grant succeeded.
SQL> CREATE USER new_users IDENTIFIED BY 123 DEFAULT TABLESPACE users TEMPORARY TABLESPACE temp;
User created.
SQL> ALTER USER new_users QUOTA 50M ON users;
User altered.
SQL> GRANT con_res_views TO new_user;
Grant succeeded.
SQL> exit
```
