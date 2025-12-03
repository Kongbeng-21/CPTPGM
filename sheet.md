⭐ MEGA CHEAT SHEET — PROGRAMMING I FINAL

(ปิยะ + ภารุจ + โครงเก่า Chawanat)
ฉบับ ultimate สำหรับสอบ Final ใน 2 วัน

🔵 PART 1 — OOP ที่ต้องรู้แบบ 100% (ปิยะ/ภารุจออกตรงนี้ทั้งหมด)
1.1 โครงสร้าง Class (จำให้แม่น)
class ClassName:
    def __init__(self, a: int, b: str):
        self.__a = a          # private
        self.b = b            # public

    def method1(self):
        ...

    def __str__(self):
        return f"{self.b}: {self.__a}"


✔ __init__ ใช้สร้าง state ของ object
✔ self.x = attribute
✔ method ที่ return ค่าต้องเขียน return ให้ถูก type
✔ โครงคลาสต้องตามสเปกคำสั่ง 100% (ห้ามเปลี่ยนชื่อ attribute/method เอง)

1.2 Encapsulation (สำคัญมาก)
private attribute
self.__balance

property
@property
def balance(self):
    return self.__balance

@balance.setter
def balance(self, value):
    if value >= 0:
        self.__balance = value


จำไว้:

UML เครื่องหมาย -balance: float = private attribute

ปรับค่า private ต้องผ่าน setter หรือ method

1.3 Inheritance (IS-A)
class Vehicle:
    def __init__(self, speed):
        self.speed = speed

    def move(self):
        return "Moving"

class Car(Vehicle):
    def __init__(self, speed, seats):
        super().__init__(speed)
        self.seats = seats

    def move(self):
        return "Driving"


📌 KEY

ต้องเรียก super().__init__()

subclass ใช้ attributes ของ parent ได้

override method → polymorphism

1.4 Polymorphism (ออกแน่นอน)
shapes = [Circle(2), Square(5)]
for s in shapes:
    print(s.get_area())     # เรียก method ต่างกันตาม class จริง

1.5 Composition (HAS-A)
class Player:
    def __init__(self, name, score):
        self.name = name
        self.score = score

class Team:
    def __init__(self, name):
        self.name = name
        self.players = []        # HAS-A relationship

    def add_player(self, p: Player):
        self.players.append(p)


📌 ออกชัวร์ในข้อ FINAL ปิยะ (ระดับใหญ่)

1.6 Command Processor Pattern (ออกบ่อยที่สุด)
while True:
    cmd = input().split()
    if cmd[0] == "exit":
        break
    elif cmd[0] == "addplayer":
        team = cmd[1]
        name = cmd[2]
        score = int(cmd[3])
        league[team].add_player(Player(name, score))
    else:
        print("Invalid command")


ต้องฝึกใช้:

cmd = input().strip().split()

cmd[0].lower()

แยกคำสั่ง + แปลง type

ตรวจความยาวก่อนใช้ index

1.7 ข้อควรระวังที่สุดของปิยะ

format output ต้องตรงทุกตัวอักษร

ช่วงคะแนน / เงื่อนไข boundary ต้องถูก

ชื่อ attribute ผิด 1 ตัว = ตรวจไม่ผ่าน

ลืม .2f = ผิดทั้งข้อ

ใน main ห้ามทำงานของ class เอง → ต้องเรียก method

🔵 PART 2 — FILE I/O + CSV + DICT (ปิยะ Final ออก 1 ข้อ)
เปิดไฟล์
with open("data.csv", "r", encoding="utf8") as f:
    for line in f:
        line = line.strip().split(",")

CSV แบบตาราง
import csv
with open("file.csv") as f:
    reader = csv.reader(f)
    header = next(reader)
    for row in reader:
        name = row[0]
        score = float(row[2])

Dict aggregate
tot = {}
cnt = {}

for name, score in data:
    tot[name] = tot.get(name, 0) + score
    cnt[name] = cnt.get(name, 0) + 1

for name in tot:
    print(name, tot[name]/cnt[name])

Error Handling
try:
    with open(file) as f:
        ...
except FileNotFoundError:
    print("Error: file not found")

🔵 PART 3 — Exception Handling (ปิยะชอบออกแบบ 10 คะแนน)
Try/Except Template
while True:
    s = input()
    try:
        x = float(s)
    except ValueError:
        print("Invalid number")
        continue

    if x < 0:
        print("Must be non-negative")
        continue

    break

ZeroDivision
try:
    result = a / b
except ZeroDivisionError:
    print("Cannot divide by zero")

🔵 PART 4 — UML Class Diagram (ภารุจออกชัวร์ 100%)

สิ่งต้องจำได้:

Symbols

+ public

- private

# protected

Relationships

IS-A (inheritance) → ลูกศรกลวงชี้ขึ้น

HAS-A (composition) → ข้าวหลามตัดทึบชี้ไปที่สิ่งที่เป็นส่วนประกอบ

Example
+ Simulation
  - balls: List<Ball>
  - digits: List<Digit>
  + run()
  + update()
  + draw()

+ Ball
  - x: float
  - y: float
  - vx: float
  - vy: float
  + update()
  + draw()

Simulation *───> Ball     (HAS-A)
Digit ─|> Ball            (IS-A กรณี inheritance)

🔵 PART 5 — FINAL ภารุจ Simulation OOP (หัวใจข้อสอบภารุจ)
ต้องสร้างคลาส:

Ball

SevenSegmentDigit

Segment

Simulation

สิ่งจำเป็น:

update() movement

bounce_if_hit_wall

draw()

main loop: while True → update → draw

UML diagram 3–4 คลาส

โครงคลาสที่ถูกต้องสุด:
class Ball:
    def __init__(self, x, y, vx, vy, r, color, bounds):
        ...
    def update(self, dt):
        ...
    def draw(self, turtle):
        ...

class Segment:
    ...
    def draw(self, t):
        ...

class SevenSegmentDigit:
    ...
    def update(self, dt):
        ...
    def draw(self, t):
        ...

class Simulation:
    def __init__(self):
        self.balls = [...]
        self.digits = [...]
    def update(self):
        ...
    def draw(self):
        ...
    def run(self):
        ...

ภารุจให้คะแนนแบบนี้:

not OOP → 0

OOP แย่ → 50

OOP ดี + UML → 100

🔵 PART 6 — Git / Version Control (อาจมี MCQ)

ต้องรู้ 10 อย่างนี้:

working directory
staging area
local repository
remote repository
git add
git commit
git push
git pull
git merge
merge conflict

Command จำ:
git add .
git commit -m "msg"
git push
git checkout -b feature
git merge feature


ถ้าต้องได้ +2 bonus → สร้าง branch แล้ว merge กลับ master

🔵 PART 7 — สิ่งที่ออกแน่นอน “จากประวัติข้อสอบปิยะ + ภารุจ”

ทั้งสองพาร์ทมีรูปแบบชัดเจนมาก

ปิยะออกแน่นอน:

OOP class + private

inheritance

composition

command processor

list of objects

formatting

simple file I/O / dict / exception (อาจ 1 ข้อใหญ่)

ภารุจออกแน่นอน:

OOP simulation

UML class diagram

movement / update loop

composition (simulation has objects)

🔵 PART 8 — สิ่งที่ควรท่องก่อนเข้าห้องสอบ (1 หน้า)
CLASS TEMPLATE
class X:
    def __init__(self, ...):
        self.__a = ...
    def method(self):
        ...

INHERITANCE
class A:
    def f(): ...
class B(A):
    def f(): ...    # override
    def __init__(...):
        super().__init__()

COMPOSITION
class Team:
    def __init__():
        self.players = []
    def add_player(p):
        self.players.append(p)

COMMAND
cmd = input().split()
if cmd[0] == "exit": break
elif cmd[0] == "add": ...

FILE I/O
with open(...) as f:
    for line in f:

CSV
import csv
reader = csv.reader(f)
header = next(reader)

DICT
d[name] = d.get(name,0) + score

EXCEPTION
try:
    ...
except ValueError:
    ...

UML
+ public
- private
A ─|> B   (inheritance)
A *─── B  (composition)

SIMULATION (ภารุจ)
update() / draw() / run()
Ball / Segment / SevenSegmentDigit / Simulation
