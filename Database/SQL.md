<div align="center">

# เอกสารประกอบการสอน
## รายวิชาสารสนเทศทางการแพทย์และการประยุกต์ใช้
## (Health Informatics and Its Applications) 

## การจัดการฐานข้อมูล SQLite ด้วยภาษา SQL

โดยอาจารย์ ดร.ลิขิต ปรียานนท์

ภาควิชาเทคนิคการแพทย์ชมุชน

คณะเทคนิคการแพทย์ มหาวิทยาลัยมหิดล

ปรับปรุงล่าสุดวันที่ 27 เม.ย. 2563
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

## การวิเคราะห์ข้อมูลตัวอย่าง Chinook Database

Chinook Database เป็นฐานข้อมูลตัวอย่างที่มีขนาดข้อมูลใหญ่มากขึ้นและมีตารางหลายตารางเหมาะสำหรับการเรียนรู้คำสั่ง SQL เบื้องต้น โครงสร้างของฐานข้อมูลดังแสดงในรูป

![chinook db](sqlite-sample-database-diagram-color.png)

### Aggregrate Functions

การวิเคราะห์ข้อมูลในฐานข้อมูลโดยส่วนมากมักจะเป็นการจัดการกับข้อมูลในภาพรวมมากกว่าข้อมูลแต่ละรายการหรือ record เช่นจำนวนลูกค้าที่มาใช้บริการในร้านค้าในแต่ละเดือนและไตรมาศเป็นต้น ซึ่งเราสามารถใช้คำสั่ง ```SELECT``` ในการเรียกดูข้อมูลและกรองข้อมูลที่ต้องการได้แต่การนับจำนวนลูกค้าโดยนับแต่ละรายการนั้นหากมีจำนวนลูกค้าจำนวนมากจะทำให้เสียเวลาและเกิดความผิดพลาดได้ง่าย **aggregate function** รับ input เป็นคอลัมน์และรายการข้อมูลหลายรายการจากนั้นให้คำตอบที่เป็นตัวเลขดังตัวอย่าง

```SQL
SELECT count(customerid) FROM customers;
```

คำตอบที่ได้คือ 59 รายการ

คำสั่ง ```COUNT``` จะนับจำนวนรายการในคอลัมน์ที่ไม่ใช่ ```NULL``` ซึ่งหากในคอลัมน์มีข้อมูลที่ขาดหายไปหรือเป็น ```NULL``` จะทำให้ไม่ทราบจำนวนรายการทั้งหมด สามารถแก้ไขได้โดยใช้คำสั่ง

```SQL
SELECT count(*) FROM customers;
```

ซึ่งในที่นี้ยังได้คำตอบเท่าเดิม เนื่องจากคอลัมน์ customerid เป็น primary key จึงไม่มีข้อมูลที่เป็น ```NULL```

aggregate function สามารถใช้งานร่วมกับ ```WHERE``` เพื่อกำหนดเงื่อนไขได้เช่นหากเราต้องการนับจำนวนลูกค้าที่มาจากประเทศสหรัฐอเมริกาเราสามารถใช้คำสั่งได้ดังนี้

```SQL
SELECT count(*) FROM customers WHERE country='USA';
```

จะได้คำตอบเท่ากับ 13

เรายังสามารถทำการคำนวณทางคณิตศาสตร์กับข้อมูลที่เราได้มาจาก aggregate function อีกด้วยดังเช่น

```SQL
SELECT count(*)*2 FROM customers WHERE country='USA';
```

จะได้คำตอบเท่ากับ $13\times2=26$

เราสามารถหาค่าต่ำสุด สูงสุด ค่าเฉลี่ยและผลรวมของข้อมูลได้ด้วยคำสั่ง ```MIN, MAX, AVG, SUM``` ตามลำดับดังนี้

```SQL
SELECT MIN(total) FROM invoices;
```

คำตอบคือ 0.99

```SQL
SELECT MAX(total) FROM invoices;
```

คำตอบคือ 25.86

```SQL
SELECT AVG(total) FROM invoices;
```

คำตอบคือ 5.65

```SQL
SELECT SUM(total) FROM invoices;
```

คำตอบคือ 2328.60

**คำถาม**

    หากนักศึกษาใช้คำสั่งข้างต้นกับข้อมูลที่ไม่ใช่ตัวเลขจะเกิดอะไรขึ้น และปัญหาจากการใช้งานฟังก์ชั่นเหล่านี้กับข้อมูลที่ไม่ใช่ตัวเลขควรป้องกันอย่างไร

### คำสั่ง ```GROUP BY```

คำสั่ง ```GROUP BY``` มีประโยชน์มากทำงานเหมือนกับการสร้าง Pivot Table ในโปรแกรมอย่างเช่น MS Excel ทำให้เราสามารถสรุปข้อมูลเพื่อวิเคราะห์ภาพรวมได้อย่างรวดเร็วโดยการจำแนกเป็นกลุ่มเช่น หากเราต้องการทราบจำนวนลูกค้าในแต่ละประเทศเราสามารถใช้คำสั่งในรูปแบบดังนี้

```SQL
SELECT key, AGGFUNC(column1) FROM table GROUP BY key
```

โดยกำหนดให้ key คือ คอลัมน์ country ดังตัวอย่าง

```SQL
SELECT country, COUNT(customerid) FROM customers GROUP BY country;
```

ผลที่ได้คือตารางรายชื่อประเทศและจำนวนลูกค้าในประเทศนั้นๆ

| Country | Count |
| --- | --- |
Argentina | 1
Australia | 1
Austria | 1
... | ...

เป็นต้น หากเราจะนับจำนวนลูกค้าที่มาจากแต่ละรัฐหรือ state เราก็สามารถใช้คอลัมน์ state เป็น key ได้ดังนี้

```SQL
SELECT state, COUNT(customerid) FROM customers GROUP BY state;
```

| State | Count |
| --- | --- |
```NULL``` | 29
AB | 1
AZ | 1
... | ...

เป็นต้น ซึ่งคำสั่ง GROUP BY ยังสามารถแบ่งกลุ่มย่อยซ้อนกันได้เหมือนกับการสร้าง Pivot Table เช่นหากเราต้องการนับจำนวนลูกค้าในแต่ละประเทศโดยจำแนกออกเป็นแต่ละรัฐด้วย เราสามารถทำได้ดังนี้

```SQL
SELECT country,state, COUNT(customerid) FROM customers GROUP BY country,state;
```

ผลที่ได้คือ

| Country | State | Count
| --- | --- | ---
Argentina | ```NULL``` | 1
... | ... | ...
USA | AZ | 1
USA | CA | 3
USA | FL | 1
... | ... | ...

นักศึกษาจะสังเกตได้ว่าข้อมูลจะเรียงตามประเทศและจากนั้นตามด้วยรัฐและจำนวนลูกค้าในแต่ละรัฐนั้นๆ

เราสามารถจัดเรียงข้อมูลได้ตามปกติเช่น หากเราต้องการเรียนข้อมูลตามประเทศจากล่างขึ้นบนหรือ Z ไป A สามารถทำได้ดังนี้

```SQL
SELECT country,state, COUNT(customerid) FROM customers GROUP by country,state ORDER BY country DESC;
```

แต่โดยส่วนมากเราอาจจะต้องการเรียงข้อมูลตามค่าที่ได้มาเช่นจำนวนนับเพื่อหารัฐที่มีลูกค้ามากที่สุด เราสามารถทำได้ดังนี้

```SQL
SELECT country,state, COUNT(customerid) FROM customers GROUP BY country,state ORDER BY count(*) DESC;
```

คำตอบคือประเทศฝรั่งเศสแต่ไม่ระบุรัฐ

เราลองมาดูคำสั่งที่ซับซ้อนมากขึ้นเช่น หากเราต้องการที่จะสรุปยอดขายทั้งหมด (total) โดยดูจากรายการในตาราง invoices สรุปตามประเทศและรัฐของลูกค้า เราสามารถใช้คำสั่ง ```INNER JOIN``` มาเชื่อมข้อมูลระหว่างตาราง customers และ invoices ดังนี้

```SQL
SELECT country,state,SUM(total) FROM invoices
INNER JOIN customers ON customers.customerid=invoices.customerid
GROUP BY country, state;
```

ผลที่ได้คือ

| Country | State | Sum
| --- | --- | ---
Argentina | ```NULL``` | 37.62
Australia | NSW | 37.62
... | ... | ...
USA | CA | 115.85

สังเกตว่าเนื่องจากเราต้องการรวมข้อมูล เราจึงใช้ฟังก์ชั่น ```SUM``` แทน ```COUNT```

ทั้งนี้หากเราต้องการสรุปเฉพาะ subset ของข้อมูลเช่น เฉพาะรัฐ CA เราสามารถเพิ่มเงื่อนไขในคำสั่งได้ด้วยคำสั่ง ```WHERE``` ดังตัวอย่าง

```SQL
SELECT country,state,SUM(total) FROM invoices
INNER JOIN customers ON customers.customerid=invoices.customerid
WHERE state='CA'
GROUP BY country, state;
```

บางครั้งเราต้องการที่จะเลือกข้อมูลโดยพิจารณาจากค่าที่ได้จากคำสั่ง ```GROUP BY``` เช่นรายการยอดรวมที่มีค่ามากกว่า $100 เป็นต้น สำหรับกรณีนี้เราไม่สามารถใช้คำสั่ง ```WHERE``` ได้แต่ต้องใช้คำสั่ง ```HAVING``` แทนดังตัวอย่าง

```SQL
SELECT country,state,SUM(total) FROM invoices
INNER JOIN customers ON customers.customerid=invoices.customerid
GROUP BY country, state
HAVING SUM(total) > 100.0;
```

ซึ่งคำตอบที่เราจะได้มีทั้งหมด 4 รายการจาก 4 ประเทศ

### แบบฝึกหัด

1. นักศึกษาจะต้องใช้คำสั่งอย่างไรจึงจะสามารถสรุปยอดการซื้อของลูกค้าแต่ละคนได้
2. หากทางร้านต้องการเสนอโปรโมชั่นให้กับลูกค้าที่มียอดซื้อสูงสุด 5 คน นักศึกษาจะหาลูกค้าทั้ง 5 คนได้อย่างไร
3. ผลงานเพลงแนวใด (genre) ที่มีจำนวนเพลง (track) มากที่สุด
4. อัลบัมได้ทำยอดขายได้มากที่สุดในร้าน 5 อันดับแรก

```SQL
select a.Title, sum(i.unitprice*i.Quantity) from tracks t
	inner join genres g on t.genreid=g.GenreId
	INNER JOIN albums a on t.AlbumId=a.AlbumId
    INNER JOIN invoice_items i on t.TrackId=i.TrackId
GROUP by a.Title ORDER BY sum(i.unitprice*i.quantity) DESC;
```

## เอกสารอ้างอิง

* [SQLite Tutorials](https://www.sqlitetutorial.net/)