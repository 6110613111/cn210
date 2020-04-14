# cn210

เป็นแหล่งรวมลิงค์ Youtube ที่สรุปเนื้อหาจากการเรียนในรายวิชา Fundamental of computer architecture หรือ cn210 (สถาปัตยกรรมคอมพิวเตออร์) โดยยึดคำสั่งของ MIPS เป็นหลัก จัดทำโดย น.ส. กนกกร นามเปรมปรีดิ

## clip1 R-format
[https://www.youtube.com/watch?v=wNY26EktrtM](https://www.youtube.com/watch?v=wNY26EktrtM)
<br>ในคลิปจะสรุป r-format โดยยกตัวอย่างเป็นคำสั่งการบวก มี 32 bit
<br>มีโครงสร้างเป็น 
| opcode(6bit) | $rs(5bit) | $rt(5bit) | $rd(5bit) | shamt(5bit) | func(6bit) |

และใน R-format opcode เป็น 000 000

และรูปแบบที่เราเข้าใจกันคือ ***func, $rd,$rs,$rt*** โดยวิธีการทำงานคือ rs คำนวนกับ rt ตามรูปแบบของ func และผลที่ได้ไปเก็บที่ rd.
## clip2 cpu
https://www.youtube.com/watch?v=S90zm02utjk&t=293s

ยกตัวอย่างการทำงานของ cumputer รูปแบบ mips ที่เริ่มจากการเปิดเครื่องการทำงานอาจจะเริ่มที่ต่ำแหน่ง 0000 00000 และทำงานตามคำสั่งต่อไปเรื่อยๆ โดยเก็บคำสั่งในรูปแบบเลขฐาน16 แบ่งที่ชุดละ 4 ตัว ซึ่งจะแปลงเป็น binary code แปลคำสั่งและทำคำสั่งนั้นๆ ไป

จากในคลิปจะการทำของ 
- R-format : คำสั่งของการคำนวน
- J-format : เป็นคำสั่งของการกระโดยให้ไปทำงานที่ต่ำแหน่งอื่นจากค่าที่กำหนด 
- I-format : โดยยกตัวอย่างของ lw กับ sw
## clip3 single cycle vs muti cycle
https://www.youtube.com/watch?v=G0OmkMiU6XA

อธิบายว่า single cycle และ muti cycle มีการทำงานอย่างไรและแตกต่างกันอย่างไร

ซึ่ง single cycle มีลักษณะเป็น
- เป็นการทำคำสั่งให้จบภายใน 1 cycle ซึ่งทำให้ต้องเผื่อเวลาสำหรับคำสั่งที่ใช้เวลานานที่สุดไว้ด้วย
- 1 cycle = 8 ns
- มี ALU 3ตัว
- มี memory 2 ตัว

ในส่วนของ muti cycle เป็น
- แบ่ง 1 cycle ใน single cycle เป็นที่ละ step โดยนับเป็น 1 cycle
- 1 cycle เวลาไม่แน่นอน
- ALU และ memory อย่างละตัว
- มี register instruction


## clip4 load word in Multi-cycle
https://www.youtube.com/watch?v=ILn1kOAwJJs

อธิบายการทำงานของ lw ใน Multi-cycle ว่ามีการทำอย่างไร มีกี่ cycle แต่ละ cycle ทำงานอย่างไร

โครงสร้าง lw จะเป็น | opcode(6bit) | $rs(5bit) | $rt(5bit) | offset(16bit) |

opcode ของlw เป็น 100011

รูปแบบที่เราเข้าใจกันคือ ***lw, $rt,offset($rs)*** 

คือ นำค่าใน rs รวมกับค่าของ offset และไปเก็บที่ rt
## clip5 BEQ in Multi-cycle
https://www.youtube.com/watch?v=Osl9eChRaCA&t=117s

อธิบายการทำงานของ BEQ ใน Multi-cycle ว่ามีการทำอย่างไร มีกี่ cycle แต่ละ cycle ทำงานอย่างไร

ซึ่ง BEQ เป็น I-format โครงสร้าง BEQ จะเป็น | opcode(6bit) | $rs(5bit) | $rt(5bit) | offset(16bit) |

มีรูปแบบที่เราเข้าใจกันคือ ***beq, $rs,$rt,offset***

คือเช็คว่า rs กับ rt เท่ากันหรือไม่ โดยวิธีการเช็คคิอนำ rs กับ rt มาลบกัน ถ้าค่าที่ได้...
- 0 ย้ายไปทำคำสั่งที่ pc + offset
- ไม่ใช่ 0 ย้ายไปทำคำสั่งที่ pc + 4
## clip6 R-type state machine
https://www.youtube.com/watch?v=Zuj5F-_kMsc

ในคลิปนี้จะอธิบายการทำของ R-type in Multi-cycle มีการอธิบายของ state machine เข้ามาร่วมด้วย

โดยเริ่มที่ 
- T1 Fetch มีค่า IorD = 0 mux จึงส่งค่าที่ได้จาก pc ไปที่ memory , ALUsrcA = 0 mux จึงส่งค่า pc ไปที่ ALU ,ALUsrcB = 1 จึงส่ง 4 ไปที่ ALU และ ALUOp = Add ที่ ALU จำคำนวนแบบบวก และส่งผลลัพธ์ไปที่ pc 
- T2 Fetch + 1 ขึ้นอยู่กับคำสั่งว่ารูปแบบไหน ถ้าเป็น R-format ก็ส่งค่า rs , rt ไปเก็บที่ A,B ถ้าเป็นคำสั่งที่ opcode จะพิจารณา state machine ด้วย
ALUsrcA = 0 mux จึงส่งค่า pc ไปที่ ALU ,ALUsrcB = 3 mux จึงส่ง offset ที่แปลงจาก 16 bit เป็น 32 bit และ shift ไป 2 ไปที่ ALU และ ALUOp = 0 ที่ ALU จำคำนวนแบบบวก และส่งผลลัพธ์ไปที่ ALUOut
- T3 ALUsrcA = 1 mux จึงส่งค่า A ไปที่ ALU ,ALUsrcB = 0 จึงส่ง B ไปที่ ALU และ ALUOp ที่รับค่าจากทั้ง OppCode และ func ส่งสัญญาณไปที่ ALU และคำนวนตามคำสั่งที่ได้มา
- T4 เป็นการนำค่าที่ได้ไปเป็นที่ rd 
## clip7 PIPELINED

อธิบาย PIPELINED โดยการเปรียบเทียบกับการซักผ้า ซึ่ง PIPELINED เข้ามาช่วยให้การทำงานของคอมพิวเตอรเร็วขึ้น เมื่อเทียบกับ single cycle และ muti cycle 
แต่ PIPELINED ก็อาจสร้างปัญหาขึ้น เช่น 
- เชิงโครงสร้าง ที่มีการซ้อนทับของวงจร 
- เชิงข้อมูล การใช้ข้อมูลจากคำสั่งก่อนหน้าแต่คำสั่งก่อนหน้ายังไม่เสร็จ 
- การควบคุม จะกระโดดแต่ติดคำสั่งก่อนหน้าเสียก่อน 

วิธีการแก้อาจจะเป็นการรอ,หรือให้คำสั่งที่มาที่หลังใช้งานอุปกรณ์ก่อน หรือจัดดับคำสั่งใหม่


