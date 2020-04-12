# cn210

เป็นแหล่งรวมลิงค์ Youtube ที่สรุปเนื้อหาจากการเรียนในรายวิชา Fundamental of computer architecture หรือ cn210 (สถาปัตยกรรมคอมพิวเตออร์) โดยยึดคำสั่งของ MIPS เป็นหลัก จัดทำโดย น.ส. กนกกร นามเปรมปรีดิ

## clip1 R-format
https://www.youtube.com/watch?v=wNY26EktrtM

ในคลิปจะสรุป r-format โดยยกตัวอย่างเป็นคำสั่งการบวก มี 32 bit

มีโครงสร้างเป็น | opcode(6bit) | $rs(5bit) | $rt(5bit) | $rd(5bit) | shamt(5bit) | func(6bit) |

และรูปแบบที่เราเข้าใจกันคือ ***func, $rd,$rs,$rt*** โดยวิธีการทำงานคือ rs คำนวนกับ rt ตามรูปแบบของ func และผลที่ได้ไปเก็บที่ rd.
## clip2 cpu
https://www.youtube.com/watch?v=S90zm02utjk&t=293s

ยกตัวอย่างการทำงานของ cumputer รูปแบบ mips ที่เริ่มจากการเปิดเครื่องการทำงานอาจจะเริ่มที่ต่ำแหน่ง 0000 00000 และทำงานตามคำสั่งต่อไปเรื่อยๆ โดยเก็บคำสั่งในรูปแบบเลขฐาน16 แบ่งที่ชุดละ 4 ตัว ซึ่งจะแปลงเป็น binary code แปลคำสั่งและทำคำสั่งนั้นๆ ไป

จากในคลิปจะการทำของ 
- R-format : คำสั่งของการคำนวน
- J-format : เป็นคำสั่งของการกระโดยให้ไปทำงานที่ต่ำแหน่งอื่นจากค่าที่กำหนด 
- I-format : โดนยกตัวอย่างของ lw กับ sw
## clip2 single cycle vs muti cycle
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
## clip3 load word in Multi-cycle
https://www.youtube.com/watch?v=ILn1kOAwJJs

อธิบายการทำงานของ lw ใน Multi-cycle ว่ามีการทำอย่างไร มีกี่ cycle แต่ละ cycle ทำงานอย่างไร

โครงสร้าง lw จะเป็น | opcode(6bit) | $rs(5bit) | $rt(5bit) | offset(16bit) |

opcode ของlw เป็น 100011

รูปแบบที่เราเข้าใจกันคือ ***lw, $rt,offset($rs)*** 

คือ นำค่าใน rs รวมกับค่าของ offset และไปเก็บที่ rt
