<div align="center">

# เอกสารประกอบการสอน
## รายวิชาสารสนเทศทางการแพทย์และการประยุกต์ใช้
## (Health Informatics and Its Applications) 

## การจัดการฐานข้อมูล SQLite ด้วยภาษา SQL

โดยอาจารย์ ดร.ลิขิต ปรียานนท์

ภาควิชาเทคนิคการแพทย์ชมุชน

คณะเทคนิคการแพทย์ มหาวิทยาลัยมหิดล
</div>

---

### ฐานข้อมูล SQLite
SQLite คือชุดโปรแกรมสำหรับจัดการระบบฐานข้อมูลชนิด relational database (relational database management system or RDBMS) ที่จัดเก็บข้อมูลในไฟล์เดียว โดยนอกจากจะระบบจัดเก็บข้อมูลที่รองรับตารางข้อมูลขนาดใหญ่แล้ว SQLite ยังสนับสนุนการเชื่อมต่อข้อมูลระหว่างตารางที่ซับซ้อนเพื่อการทำรายงานและการสรุปผลทางสถิติอีกด้วย

จุดเด่นของระบบ SQLite คือ

1. ไม่ต้องการระบบสำหรับรัน server (serverless)
2. ง่ายต่อการปรับตั้งค่าต่างๆ (zero-configuration)
3. ใช้งานได้บนระบบคอมพิวเตอร์หลากหลายชนิด (cross-platform)
4. สามารถนำไปฝังเป็นส่วนนึงของโปรแกรมที่พัฒนาเองได้ (self-contained)
5. ใช้หน่วยความจำและพื้นที่สำหรับตัวโปรแกรมน้อยเหมาะกับอุปกรณ์พกพาขนาดเล็กเช่น โทรศัพท์มือถือ ไอแพดเป็นต้น (small runtime footprint)
6. รองรับภาษา SQL อย่างสมบูรณ์ (full-featured)
7. มีความเสถียรสูง (highly reliable)

### ภาษา SQL (อ่านว่า ซี-ควึล)

Structured Query Language (SQL) เป็นภาษาที่ใช้สำหรับจัดการข้อมูลที่ฐานข้อมูลชนิด relational database ส่วนมากรองรับ ผู้ใช้สามารถใช้ภาษา SQL ในการสร้างตารางข้อมูล เรียกดูข้อมูล ลบข้อมูล ทำการสร้างดัชนีข้อมูล (indexing) หรือปรับแต่งตารางข้อมูลได้ ภาษา SQL จึงเป็นภาษาที่สำคัญที่ผู้จัดการฐานข้อมูลต้องเรียนรู้ ภาษา SQL เป็นภาษาประเภท declarative language ซึ่งผู้ใช้งานระบุสิ่งที่ต้องการหรือผลลัพธ์ที่ได้จากชุดคำสั่งจากนั้นคอมพิวเตอร์จะทำงานเพื่อให้ได้ผลลัพธ์ตามที่ผู้ใช้ต้องการ ซึ่งแตกต่างจากภาษาประเภท imperative or procedural language ที่ผู้ใช้งานต้องระบุกระบวนการอย่างเป็นขั้นตอน (procedure or algorithm) เพื่อให้คอมพิวเตอร์ทำงานให้ได้ผลลัพธ์ที่ต้องการ คำสั่งเบื้องต้นที่สำคัญของภาษา SQL คือ **CREATE TABLE, INSERT, UPDATE, DELETE** และ **SELECT** ซึ่งใช้สำหรับการสร้างตารางและกระบวนการที่เรียกว่า **CRUD (Create, Read, Update, and Delete)** เพื่อการเพิ่มข้อมูลลงในตาราง เรียกดูข้อมูลจากตารางและลบข้อมูล* โดยแรกเริ่มนั้นภาษา SQL ได้ออกแบบมาเพื่อผู้ใช้งานทั่วไปที่ไม่มีพื้นฐานทางการเขียนโปรแกรมมากนัก จึงมีรูปแบบภาษาใกล้เคียงภาษาอังกฤษ โดยมักเป็นลักษณะของคำกริยา (verb) + คำนาม (noun) เช่น **CREATE** TABLE, **DROP** INDEX, **UPDATE** table name เป็นต้น

ในการโปรแกรมด้วยภาษา SQL โดยทั่วไปนิยมใช้ตัวอักษรภาษาอังกฤษตัวพิมพ์ใหญ่สำหรับคำสั่งต่างๆ แต่ทว่าภาษา SQL เป็นภาษาที่ case-insensitive หมายถึงผู้ใช้สามารถใช้อักษรตัวพิมพ์ใหญ่หรือเล็กก็ได้ โดยความหมายยังเหมือนเดิม ภาษา SQL ใช้เครื่องหมาย semicolon (;) เพื่อระบุจุดสิ้นสุดของแต่ละบรรทัด ซึ่งสามารถละเว้นได้สำหรับคำสั่งที่มีเพียงประโยคเดียว (single statement) ช่องว่างในคำสั่งไม่มีความหมายต่อการแปลความหมายของคำสั่ง ในชุดคำสั่งเราสามารถใส่หมายเหตุได้โดยการใส่เครื่องหมาย -- หน้าบรรทัดนั้นเพื่อให้ตัวแปลภาษาข้ามการแปลภาษาของบรรทัดนั้นๆ ถ้าต้องการใส่หมายเหตุมากกว่าหนึ่งบรรทัด ให้ใส่เครื่องหมาย /* หน้าบรรทัดแรกและ */ หลังบรรทัดสุดท้าย สำหรับตัวหนังสือ ให้ใส่เครื่องหมาย ‘’ ล้อมรอบ เช่น ‘School’  ถ้าในตัวหนังสือมีเครื่องหมาย ‘ ให้ใช้ ‘’ สองอันแทนเช่น ‘O’’Reilly’ สำหรับคำว่า O’Reilly เป็นต้น

เมื่อพิมพ์คำสั่งในโปรแกรม SQLite3 interactive shell โปรแกรมจะทำงานตามคำสั่งทันที ดังนั้นหากคำสั่งมีข้อผิดพลาดในบางกรณีที่ก่อให้เกิดความเสียหายต่อข้อมูลจะไม่สามารถแก้ไขได้ ในขั้นตอนการพัฒนาฐานข้อมูลจึงควรใช้ฐานข้อมูลสำหรับการพัฒนาโดยเฉพาะ (testing database) ซึ่งเก็บสำเนาข้อมูลบางส่วนจากข้อมูลจริง หรือข้อมูลจำลองเพื่อทดสอบชุดคำสั่งก่อนนำไปใช้งานจริง

### การจัดการฐานข้อมูลพื้นฐาน: Create, Read, Update, and Delete (CRUD)

### การสร้างตาราง

ในระบบ relational database การจัดเก็บข้อมูลจะอยู่ในรูปแบบตารางซึ่งตารางจะเก็บข้อมูลของ entity โดยแต่ละ row เก็บข้อมูลของแต่ละราย ชิ้นหรืออัน (instance) ตามแต่ชนิดของ entity ซึ่งแต่ละ row ประกอบไปด้วย column ที่เก็บข้อมูล attributes คำสั่งสำหรับสร้างตารางคือ CREATE TABLE ตามด้วยชื่อตาราง ชื่อ column และผู้ใช้สามารถระบุชนิดของข้อมูลในแต่ละ column ด้วย แต่ชนิดของข้อมูลสามารถละเว้นได้
โครงสร้างพื้นฐานของคำสั่งคือ

```SQL
CREATE TABLE table_name (
    column_name column_type constraint
);
```

ทั้งนี้การตั้งชื่อตารางและ column ควรใช้ชื่อกระชับและมีความหมายสื่อถึงชนิดของข้อมูลที่ชัดเจน และนิยมใช้คำนามในรูปพหูพจน์ ชนิดของข้อมูลมีดังนี้

| Storage class | Meaning |
| --- | --- |
| NULL | ข้อมูลที่ไม่ทราบ ไม่มี (missing information or unknown) |
| INTEGER | เลขจำนวนเต็ม |
| REAL | เลขจำนวนจริง |
| TEXT | ตัวหนังสือ |
| BLOB | ย่อมาจาก binary large object สามารถเก็บข้อมูลชนิดใดก็ได้ |

เราสามารถระบุคุณสมบัติของแต่ละ column เพิ่มเติมได้โดยเติมต่อท้ายชื่อ column หรือชนิดของข้อมูล ซึ่งคุณสัมบัติอย่างหนึ่งที่สำคัญคือ PRIMARY KEY ที่กำหนดให้ column นั้นเป็น column ที่ห้ามมีค่าซ้ำกันในตารางเดียวกัน ดังตัวอย่างข้างล่าง ลูกค้าแต่ละคนที่มาตรวจสุขภาพจะมีรหัสประจำตัวที่ต่างกัน ซึ่งเราสามารถใช้เป็นค่าอ้างอิงได้ จึงจำเป็นที่เราต้องระบุคุณสมบัติ NOT NULL เพื่อไม่ให้ column นี้ไม่มีข้อมูล แต่ทว่าในกรณีที่ระบุคุณสมบัติของ column เป็น INTEGER PRIMARY KEY โปรแกรม SQLite จะกำหนดให้ column นั้นเป็น NOT NULL โดยอัตโนมัติและหากมีการเพิ่มข้อมูลโดยไม่ระบุค่าของ column นั้น SQLite จะอาศัยค่าจาก row สุดท้ายแล้วบวกเพิ่มอีก 1 ให้โดยอัตโนมัติ ในกรณีที่ต้องการให้ค่าไม่ซ้ำกันหากมีการลบข้อมูล ให้เติมคุณสมบัติ AUTOINCREMENT ไปด้วย

**ตัวอย่างที่ 1**

```SQL
CREATE TABLE customers (
	customer_id INTEGER PRIMARY KEY AUTOINCREMENT,
	firstname TEXT CHECK(firstname != ‘’), -- empty string not allowed
	lastname TEXT CHECK(lastname != ‘’), -- empty string not allowed
	gender CHAR,
	age, -- type is omitted
	created_at DEFAULT CURRENT_DATE
);
```

**ผลลัพธ์***

| customer_id (PK) | firstname (TEXT) | lastname (TEXT) | age | gender (CHAR) | created_at (Date)
| --- | --- | --- | --- | --- | --- |
| ...  | ... | ... | ... | ... | ... |

**ตัวอย่างที่ 2**

```SQL
PRAGMA foreign_keys=ON;

CREATE TABLE IF NOT EXISTS lab_results (
	glucose REAL,
	creatinine REAL,
	chol REAL,
    trig REAL,
	result_id INTEGER PRIMARY KEY AUTOINCREMENT,
	timestamp DEFAULT CURRENT_TIMESTAMP,
    customer_id INTEGER NOT NULL,
    FOREIGN KEY (customer_id)
        REFERENCES customers (id)
            ON DELETE CASCADE
            ON UPDATE NO ACTION
);

CREATE TABLE IF NOT EXISTS customers (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    firstname TEXT NOT NULL,
    lastname TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL
);
```

**ตาราง lab_results**
| result_id (PK) | glucose (REAL) | creatinine (REAL) | chol (REAL) | trig (REAL) | timestamp (DATETIME) | customer_id (FK) |
| --- | --- | --- | --- | --- | --- | --- |
| ... | ... | ... | ... | ... | ... | ... |

**ตาราง customers**
| id (PK) | firstname (TEXT) | lastname (TEXT) | email (TEXT) |
| --- | --- | --- | --- |
| ... | ... | ... | ... |

**คำอธิบายตัวอย่างที่ 2**

* PRAGMA foreign_keys=ON เป็นการตั้งค่าเพื่อให้ SQLite บังคับใช้เงื่อนไข foreign key
* IF NOT EXISTS ใช้สำหรับตรวจสอบว่าตารางนั้นยังไม่ได้ถูกสร้าง หากเราไม่ใช้คำสั่งนี้แล้วต้องการสร้างตารางที่มีอยู่แล้วจะเกิดข้อผิดพลาดได้
* DEFAULT คือระบุค่าตั้งต้น
* FOREIGN KEY เป็นการกำหนดเงื่อนไขให้ฟิลด์นั้นเป็นข้อมูลที่ปรากฎในตารางอื่น
* ON DELETE CASCADE หมายถึงหากรายการที่อ้างอิงถึงถูกลบ รายการนี้จะถูกลบด้วย
* ON UPDATE NO ACTION หมายถึงหากรายการที่อ้างอิงมีการแก้ไขข้อมูล ไม่ต้องแก้ไขรายการนี้
* UNIQUE หมายถึงฟิลด์นี้ต้องไม่ซ้ำกันในตาราง
* NOT NULL หมายถึงฟิลด์นี้ ห้ามเว้นว่าง (มีค่าเป็น NULL)

จุดที่ต้องพึงระวังคือ หลังจบชุดคำสั่งต้องลงท้ายด้วยเครื่องหมาย ```;``` เสมอ และบรรทัดก่อนเครื่องหมายวงเล็บปิด ห้ามมีเครื่องหมาย ```,```

```SQL
CREATE TABLE [IF NOT EXISTS] customers (
    id INTEGER PRIMARY KEY,
    firstname TEXT NOT NULL,
    lastname TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL, -- เครื่องหมาย , ก่อนวงเล็บปิดทำให้เกิด syntax error
);
```

คำสั่ง SQL สามารถขึ้นบรรทัดใหม่ได้หากยังไม่จบคำสั่ง เช่น

```SQL
FOREIGN KEY (customer_id)
        REFERENCES customers (id)
            ON DELETE CASCADE
            ON UPDATE NO ACTION
```

สามารถเขียนต่อกันได้ดังตัวอย่าง

```SQL
FOREIGN KEY (customer_id) REFERENCES customers (id) ON DELETE CASCADE ON UPDATE NO ACTION
```

แต่ว่าการเขียนแบบแบ่งบรรทัดจะทำให้สามารถอ่านได้ง่ายกว่าและหาข้อผิดพลาดได้ง่ายกว่า

### การเพิ่มข้อมูลลงตาราง

รูปแบบคำสั่งสำหรับการเพิ่มข้อมูลลงตารางมีดังนี้

```SQL
INSERT INTO table (column1, column2,...) VALUES (value1, value2,...);
```

**ตัวอย่างที่ 3**

```SQL
INSERT INTO customers (firstname, lastname, email)
VALUES ('John', 'Doe', 'doe@gmail.com');
```

**ตาราง customers**
| id (PK) | firstname (TEXT) | lastname (TEXT) | email (TEXT) |
| --- | --- | --- | --- |
| 1 | John | Doe | doe@gmail.com |


เราสามารถเพิ่มข้อมูลหลายๆ รายการได้พร้อมกันดังนี้
```SQL
INSERT INTO customers (firstname, lastname, email)
VALUES
    ('Jane', 'Doe', 'janedoe@gmail.com'),
    ('Don', 'Corleone', 'corleonefam@hotmail.com'),
    ('Mozart', 'McWell', 'mcwell@yahoo.com')
    ;
```

### การเลือกดูข้อมูลจากตาราง
เราสามารถเลือกดูข้อมูลที่เราเพิ่มในรายการได้ด้วยรูปแบบคำสั่งดังนี้

```SQL
SELECT (columns) FROM table;
```

**ตัวอย่างที่ 4**

```SQL
SELECT * FROM customers;
```

```*``` หมายถึงเลือกทุกคอลัมน์

**ตาราง customers**
| id (PK) | firstname (TEXT) | lastname (TEXT) | email (TEXT) |
| --- | --- | --- | --- |
| 1 | John | Doe | doe@gmail.com |
| 2 | Jane | Doe | janedoe@gmail.com |
| 3 | Don | Corleone | corleonefam@hotmail.com |
| 4 | Mozart | McWell | mcwell@yahoo.com |

เราสามารถเรียงลำดับข้อมูลตามคอลัมน์ที่เราต้องการได้ด้วยคำสั่ง ```ORDER BY``` ดังนี้

**ตัวอย่างที่ 5**

```SQL
SELECT lastname,firstname,email FROM customers ORDER BY lastname;
```
**ตาราง customers**
| id (PK) | lastname (TEXT) | firstname (TEXT) | email (TEXT) |
| --- | --- | --- | --- |
| 3 | Corleone | Don | corleonefam@hotmail.com |
| 1 | Doe | John | doe@gmail.com |
| 2 | Doe | Jane | janedoe@gmail.com |
| 4 | McWell | Mozart | mcwell@yahoo.com |

หรือเราจะกรองเฉพาะจำนวนรายการที่ต้องการด้วยคำสั่ง ```LIMIT```

**ตัวอย่างที่ 6**

```SQL
SELECT lastname,firstname,email FROM customers ORDER BY lastname LIMIT 2;
```

**ตาราง customers**
| id (PK) | lastname (TEXT) | firstname (TEXT) | email (TEXT) |
| --- | --- | --- | --- |
| 3 | Corleone | Don | corleonefam@hotmail.com |
| 1 | Doe | John | doe@gmail.com |

เราสามารถกรองเฉพาะรายการที่ตรงเงื่อนไขได้ด้วยคำสั่ง ```WHERE``` เช่น

**ตัวอย่างที่ 7**

```SQL
SELECT lastname,firstname,email FROM customers WHERE lastname='Doe' ORDER BY lastname;
```

ข้อพึงระวังคือคำสั่ง ```WHERE``` ต้องมาก่อนคำสั่ง ```ORDER BY```

**ตาราง customers**
| id (PK) | lastname (TEXT) | firstname (TEXT) | email (TEXT) |
| --- | --- | --- | --- |
| 1 | Doe | John | doe@gmail.com |
| 2 | Doe | Jane | janedoe@gmail.com |

### การแก้ไขข้อมูล

เราสามารถแก้ไขข้อมูลในตารางด้วยคำสั่ง ```UPDATE``` ดังนี้

```SQL
UPDATE
    SET column_1 = new_value_1,
        column_2 = new_value_2
    WHERE
        search_condition
    ;
```

**ตัวอย่างที่ 8**

```SQL
UPDATE customers SET email='jdoe@gmail.com' WHERE id=2;
```

**ตาราง customers**
| id (PK) | lastname (TEXT) | firstname (TEXT) | email (TEXT) |
| --- | --- | --- | --- |
| 2 | Doe | Jane | jdoe@gmail.com |


### การเลือกแสดงข้อมูลที่เชื่อมโยงกันระหว่างตาราง

เราสามารถแสดงข้อมูลที่เชื่อมโยงกันได้ด้วยคำสั่ง ```JOIN``` โดยมีรูปแบบดังนี้

```SQL
SELECT columns FROM table1 INNER JOIN table2 ON table1.key=table2.key;
```

แต่ก่อนที่เราจะเชื่อมโยงข้อมูล เราต้องเพิ่มรายการข้อมูลลงในตาราง lab_results ก่อนดังนี้

**ตัวอย่างที่ 9**
```SQL
INSERT INTO lab_results (glucose,creatinine,chol,trig,customer_id)
VALUES (120,5.5,230,350,1),(110,4.6,190,300,2);
```

**ตาราง lab_results**
| result_id (PK) | glucose (REAL) | creatinine (REAL) | chol (REAL) | trig (REAL) | timestamp (DATETIME) | customer_id (FK) |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 120 | 5.5 | 230 | 350 | 2020-04-20 01:52:23 | 1 |
| 2 | 110 | 4.6 | 190 | 300 | 2020-04-20 01:52:23 | 2 |


จากนั้นเลือกแสดงข้อมูลทั้งสองตารางดังนี้

**ตัวอย่างที่ 10**
```SQL
SELECT * from lab_results INNER JOIN customers on lab_results.customer_id=customers.id;
```

**ตาราง lab_results**
| result_id (PK) | glucose (REAL) | creatinine (REAL) | chol (REAL) | trig (REAL) | timestamp (DATETIME) | customer_id (FK) | id | firstname | lastname | email |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 120 | 5.5 | 230 | 350 | 2020-04-20 01:52:23 | 1 | 1 | John | Doe | doe@gmail.com |
| 2 | 110 | 4.6 | 190 | 300 | 2020-04-20 01:52:23 | 2 | 2 | Jane | Doe | jdoe@gmail.com |

**ตัวอย่างที่ 11**
```SQL
SELECT glucose,firstname,lastname,email FROM lab_results INNER JOIN customers on lab_results.customer_id=customers.id;
```

**ตาราง lab_results**
| glucose (REAL) | firstname | lastname | email | timestamp |
| --- | --- | --- | --- | --- | 
| 120 | John | Doe | doe@gmail.com | 2020-04-20 01:52:23 |
| 110 | Jane | Doe | jdoe@gmail.com | 2020-04-20 01:52:23 |

ในบางกรณีชื่อคอลัมน์ระหว่างตารางอาจจะซ้ำกันได้ เราสามารถแก้ไขได้โดยระบุชื่อสำหรับใช้เรียกแทนชื่อตาราง (alias) ดังนี้

**ตัวอย่างที่ 12**
```SQL
SELECT l.glucose,c.firstname,c.lastname,c.email FROM lab_results l
INNER JOIN customers c on l.customer_id=c.id;
```

ซึ่งค่าที่ได้จะเท่ากับตารางที่แสดงก่อนหน้านี้

### การลบรายการข้อมูลจากตาราง

เราสามารถใช้คำสั่ง ```DELETE FROM``` สำหรับลบข้อมูลจากตารางได้ดังตัวอย่าง


**ตัวอย่างที่ 13**
```SQL
DELETE FROM customers WHERE id=2;
```

สังเกตว่าเนื่องจากเราตั้งค่า ```ON DELETE CASCADE``` ดังนั้นเมื่อเราลบรายการ customers รายการผลการทดสอบที่เกี่ยวข้องกับผู้รับบริการรายนั้นจะถูกลบไปด้วย


## เอกสารอ้างอิง

* [SQLite Tutorials](https://www.sqlitetutorial.net/)