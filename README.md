# cn210

เป็นแหล่งรวมลิงค์ Youtube ที่สรุปเนื้อหาจากการเรียนในรายวิชา Fundamental of computer architecture หรือ cn210 (สถาปัตยกรรมคอมพิวเตออร์) โดยยึดคำสั่งของ MIPS เป็นหลัก จัดทำโดย น.ส. กนกกร นามเปรมปรีดิ

## clip1 R-format
https://www.youtube.com/watch?v=wNY26EktrtM

ในคลิปจะสรุป r-format โดยยกตัวอย่างเป็นคำสั่งการบวก มี 32 bit

มีโครงสร้างเป็น | opcode(6bit) | $rs(5bit) | $rt(5bit) | $rd(5bit) | shamt(5bit) | func(6bit) |

และรูปแบบที่เราเข้าใจกันคือ *func, $rd,$rs,$rt*

โดยวิธีการทำงานคือ rs คำนวนกับ rt ตามรูปแบบของ func และผลที่ได้ไปเก็บที่ rd.
## clip2 cpu
https://www.youtube.com/watch?v=S90zm02utjk&t=293s
