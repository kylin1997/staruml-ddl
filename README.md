本项目基于原作者starUML的 ddl的插件进行修改。 
对MySQL进行了更加完善的适配。

增加了主键自增，字段注释，表注释。


插件路径：

MacOS： /Users/<your user>/Library/Application Support/StarUML/extensions/

Window: C:\Users/<your user>\AppData\Roaming\StarUML\extensions\

Linux: ~/.config/StarUML/extensions/

可将整个文件夹放到对应系统的Extensions目录。


DDL Extension for StarUML 3.0
=========================
This extension contain AUTO_INCREMENT, COMMENT, DEFAULT VALUE FOR DATE COLUMN

This extension for StarUML (http://staruml.io) support to generate DDL (Data Definition Language) from ERD. Install this extension from Extension Manager of StarUML.

How to use
----------

1. Click the menu (`Tools > DDL > Generate DDL...`)
2. Select a data model that will be generated to DDL.
3. Save the generated DDL to a file.

Generation rules
----------------

Belows are the rules to convert from ERD elements to DDL.

* All entities and columns are converted to create table statements as follow:

```sql
CREATE TABLE entity1 (
    col1 INTEGER,
    col2 VARCHAR(20),
    ...
);
```

* Primary keys are converted as follow:

```sql
CREATE TABLE entity1 (
    pk1 INTEGER,
    pk2 VARCHAR(10),
    ...
    PRIMARY KEY (pk1, pk2, ...)
);
```

* Not-nullable columns are converted as follow:

```sql
CREATE TABLE entity1 (
    col1 VARCHAR(20) NOT NULL,
    ...
);
```

* Unique columns are converted as follow:

```sql
CREATE TABLE entity1 (
    ...
    UNIQUE (col1, col2, ...)
);
```

* Foreign keys are converted as follow:

```sql
CREATE TABLE entity1 (
    fk1 INTEGER,
    ...
);
...

ALTER TABLE entity1 ADD FOREIGN KEY (fk1) REFERENCES entity2(col1);
```

* If `Quote Identifiers` option is selected, all identifiers will be surrounded by a backquote character.

```sql
CREATE TABLE `entity1` (
    `col1` INTEGER,
    `col2` VARCHAR(20),
    ...
);
```

* If `Drop Tables` option is selected, drop table statements will be included.

(__MySQL__ selected in `DBMS` option)
```sql
SET FOREIGN_KEY_CHECKS = 0;
DROP TABLE IF EXISTS entity1;
...
SET FOREIGN_KEY_CHECKS = 1;

CREATE TABLE entity1 (...);
...
```

(__Oracle__ selected in `DBMS` option)
```sql
DROP TABLE entity1 CASCADE CONSTRAINTS;`
...

CREATE TABLE entity1 (...);
...
```


Contributions
-------------

Any contributions are welcome. If you find a bug or have a suggestion, please post as an issue.
