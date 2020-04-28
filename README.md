# cn210 
## สรุปการเรียนวิชา cn210 จัดทำโดย น.ส.กนกกร นามเปรมปรีดิ์ 6110613301

<br>ส่วนประกอบ computer มี 3 ส่วน
- CPU : หน่วยประมวลผลกลาง
- Main Memory : หน่วยความจำหลัก
- I/O : หน่วยรับข้อมูลเข้าออก

ซึ่ง CPU ประกอบด้วย 3 ส่วย
- ALU : คำนวนทางคณิตศาสตร ตรรกศาสตร์
- Register : ที่พักความจำชั่วคราว
- Control Unit : หน่วยควยคุม

<br>MIPS Instruction เป็นสถาปัตยกรรมชุดคำสั่ง ที่มีขนาด 32bit ทุกคำสั่ง การแปลงคำสั่งดูได้จาก
**ALU DECODER**
<br>![img](https://i.imgur.com/0DEre3p.jpg)

ซึ่ง MIPS Instruction แบ่งออกเป็น 3 format

**1) R-format : เกี่บวกับการคำนวน**

|    opcode    |      $rs     |     $rt      |      $rd     |    shamt     |     func     |
|--------------|--------------|--------------|--------------|--------------|--------------|
|    (6bit)    |    (5bit)    |   (5bit)     |    (5bit)    |   (5bit)     |    (6bit)    |

ลักษณะการทำงานจะเป็น
<br>![img](https://i.imgur.com/axkI8r9.jpg)

**2) I-format : เกี่ยวกับหน่วยความจำ**

|    opcode    |      $rs     |     $rt      |        offset          |
|--------------|--------------|--------------|------------------------|
|    (6bit)    |    (5bit)    |   (5bit)     |         (16bit)        |

- ลักษณะการทำงานของ lw จะเป็น
<br>![img](https://i.imgur.com/4pxPfj8.jpg)
<br>นำdataของaddress ที่เกิดจาก นำ dataใน rs + offset และไปเก็บที่ rt

- ลักษณะการทำงานของ sw จะเป็น
<br>![img](https://i.imgur.com/8mgsz3d.jpg)
<br>นำdataของaddress rt ไปเก็บที่ address ที่เกิดจากการนำ dataใน rs + offset

- ลักษณะการทำงานของ beq จะเป็น
<br>![img](https://i.imgur.com/xEYYU7A.jpg)
<br> เช็ค data ใน rs กับ data ใน rt เท่ากันหรือไม่ หากเท่ากัน ต่ำแหน่งที่ทำคำสั่งต่อไปคือ offset shift ไป 2 และไปบวกกับ pc หากไม่เท่าจะทำที่ต่ำแหน่ง pc+4

**3) J-format : กระโดดไปที่ตำแหน่งที่ระบุ**

|    opcode    |      absolute address    |
|--------------|--------------------------|
|     (6bit)   |         (26bit)          |

<br>---------------------------------------------<br>
**von neumann architecture** : ใช้พื้นที่น้อย และ แก้ไขโปรแกรมง่าย แต่โปรแกรมก็จะถูกเขียนทับง่าย และใช้ Bandwidth สูงเพราะ instruction กับ data ใช้ memory เดียวกัน
<br>![img](https://i.imgur.com/jELt2xE.jpg)

พัฒนามาเป็น
**Harvard architecture** : มีความเร็วมากว่า von neumann แต่เขียนโปรแกรมยากกว่า เพราะ instruction กับ data แยกmemory ออกจากกัน
<br>![img](https://i.imgur.com/uU9GSAk.jpg)
<br> *และมีการพัฒนามาเป็น Modified Harvard Architecture ที่รวมข้อดีไว้ด้วยกัน

<br>---------------------------------------------<br> 

**Single cycle** : แต่ละคำสั่งต้องจบภายใน 1 cycle ซึ่งเท่ากับ 1 clock = 8 ns หากคำสั่งไหนที่เสร็จก่อน 8ns จะต้องให้ครบ 8ns ก่อนทำให้เกิดเวลาที่เป็น waste 
<br>![img](https://i.imgur.com/qOTAKYp.jpg)

ซึ่งพัฒนามาเป็น **multi cycle** แบ่ง step ใน Single cycle เป็น 1 cycle ทำให้เวลาที่เป็น waste มาใช้แทนที่จะสูญเสียโดยเปล่าประโยชน์
<br>![img](https://i.imgur.com/EchLi1X.jpg)
<br>multi cycle ทำสูงสุดที่ 5 cycle แบ่งออกเป็น
- T1 i-fecth : ส่งคำสั่งไปที่ memory และ pc + 4
- T2 i-fecth +1 : แปลคำสั่ง
- T3 Exex : คำนวน
- T4 ส่งไปที่ mem
- T5 เขียนลง mem

และพัฒนามาเป็น pipelined ที่เป็นการ 1 คำสั่งเป็นแบบ multicycle แต่มีความเร็วมากขึ้น
![img](https://i.imgur.com/32s6Haz.jpg)

<br>---------------------------------------------<br>

| **CISC** | **RISC** |
|--------|--------|
|ซับซ้อน|เรียบง่าย|
|มีชุดคำสั่งเยอะ|คำชุดสั่งน้อย|
|มีคำสั่งเข้า memory มากกว่า lw & sw|มีคำสั่งเข้า memory 'แค่' lw & sw|
|instruction สามารถเปลี่ยนแปลงได้|instruction ขนาดคงที่|
|multi cycle|single cycle|

<br>---------------------------------------------<br>

## [clip1 R-format](https://www.youtube.com/watch?v=wNY26EktrtM)
<br>ในคลิปจะสรุป r-format โดยยกตัวอย่างเป็นคำสั่งการบวก มี 32 bit
<br>มีโครงสร้างเป็น 

|    opcode    |      $rs     |     $rt      |      $rd     |    shamt     |     func     |
|--------------|--------------|--------------|--------------|--------------|--------------|
|    (6bit)    |    (5bit)    |   (5bit)     |    (5bit)    |   (5bit)     |    (6bit)    |

และใน R-format opcode เป็น 000 000
<br>ซึ่งรูปแบบที่เราเข้าใจกันคือ ***func, $rd,$rs,$rt*** 
<br>โดยวิธีการทำงานคือ rs คำนวนกับ rt ตามรูปแบบของ func และผลที่ได้ไปเก็บที่ rd.


## [clip2 cpu](https://www.youtube.com/watch?v=S90zm02utjk)
<br>ยกตัวอย่างการทำงานของ cumputer รูปแบบ mips ที่เริ่มจากการเปิดเครื่องการทำงานอาจจะเริ่มที่ต่ำแหน่ง 0000 00000 
<br>และทำงานตามคำสั่งต่อไปเรื่อยๆ โดยเก็บคำสั่งในรูปแบบเลขฐาน16 แบ่งที่ชุดละ 4 ตัว 
<br>ซึ่งจะแปลงเป็น binary code แปลคำสั่งและทำคำสั่งนั้นๆ ไป
<br>จากในคลิปจะอธิบายการทำงานของ 
- R-format : คำสั่งของการคำนวน
- J-format : เป็นคำสั่งของการกระโดยให้ไปทำงานที่ต่ำแหน่งอื่นจากค่าที่กำหนด 
- I-format : โดยยกตัวอย่างของ lw กับ sw

## [clip3 single cycle vs muti cycle](https://www.youtube.com/watch?v=G0OmkMiU6XA)
<br>อธิบายว่า single cycle และ muti cycle มีการทำงานอย่างไรและแตกต่างกันอย่างไร

| type/feature |       1cycle      |  time/cycle  |      ALU     |    memory    |instruction register|
|--------------|-------------------|--------------|--------------|--------------|--------------|
|    single    |      finished     |      8ns     |       3      |       2      |       0      |
|    multi     |no need to finished|   Uncertain  |       1      |       1      |       1      |


## [clip4 load word in Multi-cycle](https://www.youtube.com/watch?v=ILn1kOAwJJs)
<br>อธิบายการทำงานของ lw ใน Multi-cycle ว่ามีการทำอย่างไร มีกี่ cycle แต่ละ cycle ทำงานอย่างไร
<br>โครงสร้าง lw จะเป็น 
 
|    opcode    |      $rs     |     $rt      |      offset(16bit)     |
|--------------|--------------|--------------|------------------------|
|    (6bit)    |    (5bit)    |   (5bit)     |         (16bit)        |

opcode ของlw เป็น 100011
<br>รูปแบบที่เราเข้าใจกันคือ ***lw, $rt,offset($rs)*** 
<br>คือ นำค่าใน rs รวมกับค่าของ offset และไปเก็บที่ rt

## [clip5 BEQ in Multi-cycle](https://www.youtube.com/watch?v=Osl9eChRaCA)
<br>อธิบายการทำงานของ BEQ ใน Multi-cycle ว่ามีการทำอย่างไร มีกี่ cycle แต่ละ cycle ทำงานอย่างไร
<br>ซึ่ง BEQ เป็น I-format โครงสร้าง BEQ จะเป็น 

|    opcode    |      $rs     |     $rt      |      offset(16bit)     |
|--------------|--------------|--------------|------------------------|
|    (6bit)    |    (5bit)    |   (5bit)     |         (16bit)        |

มีรูปแบบที่เราเข้าใจกันคือ ***beq, $rs,$rt,offset***
<br>คือเช็คว่า rs กับ rt เท่ากันหรือไม่ โดยวิธีการเช็คคิอนำ rs กับ rt มาลบกัน ถ้าค่าที่ได้...
- 0 ย้ายไปทำคำสั่งที่ pc + offset
- ไม่ใช่ 0 ย้ายไปทำคำสั่งที่ pc + 4


## [clip6 R-type state machine](https://www.youtube.com/watch?v=Zuj5F-_kMsc)
<br>ในคลิปนี้จะอธิบายการทำของ R-type in Multi-cycle มีการอธิบายของ state machine เข้ามาร่วมด้วย
<br>โดยเริ่มที่ 

```
T1 : Fetch มีค่า IorD = 0 mux จึงส่งค่าที่ได้จาก pc ไปที่ memory , ALUsrcA = 0 mux 
จึงส่งค่า pc ไปที่ ALU ,
ALUsrcB = 1 จึงส่ง 4 ไปที่ ALU และ ALUOp = Add ที่ ALU จำคำนวนแบบบวก และส่งผลลัพธ์ไปที่ pc 

T2 Fetch + 1 ขึ้นอยู่กับคำสั่งว่ารูปแบบไหน ถ้าเป็น R-format ก็ส่งค่า rs , rt ไปเก็บที่ A,B 
ถ้าเป็นคำสั่งที่ opcode จะพิจารณา state machine ด้วย ALUsrcA = 0 mux จึงส่งค่า pc ไปที่ ALU ,
ALUsrcB = 3 mux จึงส่ง offset ที่แปลงจาก 16 bit เป็น 32 bit 
และ shift ไป 2 ไปที่ ALU และ ALUOp = 0 ที่ ALU จำคำนวนแบบบวก และส่งผลลัพธ์ไปที่ ALUOut

T3 ALUsrcA = 1 mux จึงส่งค่า A ไปที่ ALU ,ALUsrcB = 0 จึงส่ง B ไปที่ ALU และ 
ALUOp ที่รับค่าจากทั้ง OppCode และ func ส่งสัญญาณไปที่ ALU และคำนวนตามคำสั่งที่ได้มา

T4 เป็นการนำค่าที่ได้ไปเป็นที่ rd โดย memtoreg = 0 ค่าที่เข้าmemคือALUout 
, regDst = 1 ค่าที่เข้าไป IR  $rd(เป็นการระบุ rigister ว่าให้เซฟให้ตัวไหน) 
และ RegWrite = 1 คือให้ เขียนค่าของ ALUout ลง $rd
```

## [clip7 PIPELINED](https://www.youtube.com/watch?v=Tuu2xxzDl2Q)
<br>อธิบาย PIPELINED โดยการเปรียบเทียบกับการซักผ้า 
<br>PIPELINED คือการที่คำสั่งแรกไม่จำเป็นต้องทำเสร็จก่อนคำสั่งที่สองก็ทำต่อได้เลย 
<br>พราะบ้างครั้ง step ก่อนหน้า กับ step ถัดไปมีการใช้อุปกรณ์คนละตัว ทำให้อุปกรณว่างให้คำสั่งถัดไปได้ทำงานได้เลย 
<br>เมื่อ computer นำหลักนี้เข้ามาใช้ทำให้การทำงานของคอมพิวเตอรเร็วขึ้น เมื่อเทียบกับ single cycle และ muti cycle 
<br>แต่ PIPELINED ก็อาจสร้างปัญหาขึ้น เช่น 
- เชิงโครงสร้าง ที่มีการซ้อนทับของวงจร 
- เชิงข้อมูล การใช้ข้อมูลจากคำสั่งก่อนหน้าแต่คำสั่งก่อนหน้ายังไม่เสร็จ 
- การควบคุม จะกระโดดแต่ติดคำสั่งก่อนหน้าเสียก่อน 

วิธีการแก้อาจจะเป็นการรอ,หรือให้คำสั่งที่มาที่หลังใช้งานอุปกรณ์ก่อน หรือจัดดับคำสั่งใหม่


