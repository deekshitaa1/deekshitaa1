<div align="center">

<img src="assets/profile-photo.png" width="300" alt="Deekshita Rajesh — profile photo">

<br>

<a href="https://github.com/deekshitaa1">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=26&duration=2600&pause=900&color=E91E63&center=true&vCenter=true&width=650&lines=Deekshita+Rajesh;Software+Development+Engineer;Backend+%26+API+Development;Data+Structures+%26+Algorithms;System+Design+%26+Cloud;01010011+01000100+01000101" alt="typing banner">
</a>

<br>

<a href="https://www.linkedin.com/in/deekshita-rajesh">
  <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn">
</a>
<a href="mailto:deekshitarajesh1@gmail.com">
  <img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email">
</a>
<a href="https://deekshita-portfolio-one.vercel.app/">
  <img src="https://img.shields.io/badge/Portfolio-111111?style=for-the-badge&logo=githubpages&logoColor=white" alt="Portfolio">
</a>
<a href="https://leetcode.com/u/deekshiarajesh/">
  <img src="https://img.shields.io/badge/LeetCode-FFA116?style=for-the-badge&logo=leetcode&logoColor=white" alt="LeetCode">
</a>

</div>



</div>



from PIL import Image, ImageDraw, ImageFont, ImageFilter
import os, math, zipfile

base="/mnt/data/sde_snake_ladder_readme"
assets=os.path.join(base,"assets")
os.makedirs(assets,exist_ok=True)
W,H=1000,620
N=48
reg="/usr/share/fonts/truetype/dejavu/DejaVuSans.ttf"
bold="/usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf"
def ft(s,b=False): return ImageFont.truetype(bold if b else reg,s)

def draw_glow(im,x,y,r,rgba,blur=18):
    layer=Image.new("RGBA",im.size,(0,0,0,0))
    ImageDraw.Draw(layer).ellipse((x-r,y-r,x+r,y+r),fill=rgba)
    im.alpha_composite(layer.filter(ImageFilter.GaussianBlur(blur)))

frames=[]
for f in range(N):
    im=Image.new("RGBA",(W,H),(25,15,22,255))
    haze=Image.new("RGBA",(W,H),(0,0,0,0))
    hd=ImageDraw.Draw(haze)
    hd.ellipse((80,70,930,600),fill=(175,75,111,32))
    hd.ellipse((300,100,800,520),fill=(224,166,119,19))
    im.alpha_composite(haze.filter(ImageFilter.GaussianBlur(90)))
    d=ImageDraw.Draw(im)
    d.text((46,28),"THE SDE CLIMB",font=ft(22,True),fill=(255,221,232,255))
    d.text((48,61),"A LITTLE SNAKE. A BIG SYSTEM. SHIP IT ANYWAY.",font=ft(11,True),fill=(220,179,190,255))
    # board perspective
    left,top=190,135
    cw,ch=82,65
    # board outer shadow / frame
    d.rounded_rectangle((left-16,top-16,left+10*cw+16,top+6*ch+16),radius=18,fill=(47,25,36,255),outline=(207,145,159,220),width=3)
    # cells 1..60 in serpentine rows
    for row in range(6):
        for col in range(10):
            x=left+col*cw; y=top+row*ch
            num=row*10+(col+1) if row%2==0 else row*10+(10-col)
            fill=(82,43,59,255) if (row+col)%2==0 else (105,58,73,255)
            d.rounded_rectangle((x+2,y+2,x+cw-2,y+ch-2),radius=6,fill=fill,outline=(166,105,124,190),width=1)
            d.text((x+9,y+7),f"{num:02d}",font=ft(10,True),fill=(245,214,220,220))
    # ladder from lower-left to upper-middle
    def ladder(p1,p2):
        x1,y1=p1; x2,y2=p2
        d.line((x1-9,y1,x2-9,y2),fill=(255,214,155,255),width=5)
        d.line((x1+9,y1,x2+9,y2),fill=(255,214,155,255),width=5)
        for t in [k/8 for k in range(1,8)]:
            x=x1+(x2-x1)*t; y=y1+(y2-y1)*t
            d.line((x-10,y,x+10,y),fill=(255,235,194,255),width=3)
    ladder((left+cw*1.5,top+ch*5.25),(left+cw*4.2,top+ch*2.0))
    ladder((left+cw*6.0,top+ch*4.5),(left+cw*8.0,top+ch*1.2))
    # snake curve with animated head
    pts=[]
    for k in range(100):
        t=k/99
        x=left+cw*(8.9-5.7*t)
        y=top+ch*(0.6+4.5*t)+math.sin(t*math.pi*4+f*2*math.pi/N)*8
        pts.append((x,y))
    d.line(pts,fill=(230,130,158,255),width=13,joint="curve")
    d.line(pts,fill=(255,193,208,255),width=3,joint="curve")
    hx,hy=pts[0]
    draw_glow(im,int(hx),int(hy),19,(255,135,174,130),18)
    d=ImageDraw.Draw(im)
    d.ellipse((hx-13,hy-13,hx+13,hy+13),fill=(255,174,195,255),outline=(255,232,236,255),width=2)
    d.ellipse((hx-5,hy-4,hx-2,hy-1),fill=(72,29,48,255))
    d.ellipse((hx+3,hy-4,hx+6,hy-1),fill=(72,29,48,255))
    # token moves along serpentine path 1..60
    step=(f/(N-1))*59
    r=int(step)//10; c=int(step)%10
    if r%2==1: c=9-c
    tx=left+(c+.5)*cw; ty=top+(r+.5)*ch
    draw_glow(im,int(tx),int(ty),20,(255,218,160,180),20)
    d=ImageDraw.Draw(im)
    d.ellipse((tx-11,ty-11,tx+11,ty+11),fill=(255,226,177,255),outline=(255,250,229,255),width=2)
    # side panel
    d.rounded_rectangle((48,145,160,525),radius=15,fill=(49,27,38,230),outline=(173,105,129,180),width=1)
    d.text((65,170),"LEVEL",font=ft(10,True),fill=(224,173,191,255))
    d.text((65,195),"SDE",font=ft(22,True),fill=(255,226,233,255))
    d.line((65,238,142,238),fill=(173,105,129,180),width=1)
    d.text((65,260),"BUGS",font=ft(10,True),fill=(224,173,191,255))
    d.text((65,282),"0*",font=ft(22,True),fill=(255,226,233,255))
    d.text((65,330),"BUILDS",font=ft(10,True),fill=(224,173,191,255))
    d.text((65,352),"∞",font=ft(25,True),fill=(255,226,233,255))
    d.text((65,420),"*IN THEORY",font=ft(8),fill=(202,164,176,255))
    d.rounded_rectangle((left,545,970,592),radius=12,fill=(48,27,38,235),outline=(194,132,150,150),width=1)
    d.text((left+18,559),"CLIMB: TESTS PASS  →  DEPLOY",font=ft(12,True),fill=(255,224,231,255))
    d.text((720,559),"SLIDE: UNCAUGHT EXCEPTION",font=ft(10,True),fill=(255,193,168,255))
    frames.append(im.convert("RGB"))

gif=os.path.join(assets,"sde-snake-ladder.gif")
frames[0].save(gif,save_all=True,append_images=frames[1:],duration=100,loop=0,optimize=True)

readme=r'''<!-- REPLACE FROM YOUR EXISTING `~/ whoami` SECTION TO THE END WITH THIS CONTENT.
     Keep the profile photo, typing banner, social links and all content ABOVE whoami unchanged. -->

---

## `~/` whoami

```console
$ whoami
Deekshita Rajesh

$ role --target
Software Development Engineer

$ engineering --focus
Data Structures · Backend Systems · API Design · Reliability

$ objective
Build correct, maintainable software. Understand the trade-offs. Ship with confidence.
```

I enjoy solving engineering problems from first principles: choosing the right data structures, designing clear interfaces, building dependable backend services, and testing how systems behave when things go wrong.

> **Good code gets it working. Good engineering makes it dependable.**

---

## `~/` the engineering game

<div align="center">
  <img src="assets/sde-snake-ladder.gif" width="100%" alt="Animated blush pink and chocolate wine SDE snake and ladder board">
  <sub>ROLL THE DICE · SOLVE THE BUG · CLIMB THE LADDER · SHIP THE BUILD</sub>
</div>

<table>
  <tr>
    <td width="50%" valign="top">
      <strong>🪜 THE LADDER — LEVEL UP</strong><br><br>
      `DSA` → `OOP` → `Design` → `Implementation` → `Testing` → `Deployment`
    </td>
    <td width="50%" valign="top">
      <strong>🐍 THE SNAKE — REAL-WORLD SURPRISES</strong><br><br>
      Off-by-one errors · Race conditions · Failed tests · Slow queries · Unexpected input
    </td>
  </tr>
</table>

<sub>Game rule: every bug is a lesson; every passing test is one step up. No production database was harmed in this game.</sub>

---

## `~/` technical skills

<table>
  <tr>
    <td width="50%" valign="top">
      <strong>PROGRAMMING LANGUAGES</strong><br><br>
      <code>Python</code> <code>TypeScript</code>
    </td>
    <td width="50%" valign="top">
      <strong>COMPUTER SCIENCE FUNDAMENTALS</strong><br><br>
      <code>Data Structures & Algorithms</code><br>
      <code>Algorithm Design</code><br>
      <code>Object-Oriented Programming</code><br>
      <code>Object-Oriented Design</code><br>
      <code>Problem Solving</code><br>
      <code>Time & Space Complexity Analysis</code>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <strong>SOFTWARE ENGINEERING</strong><br><br>
      <code>Software Development Life Cycle</code><br>
      <code>Software Design</code> · <code>Design Patterns</code><br>
      <code>Distributed Systems</code><br>
      <code>RESTful API Development</code><br>
      <code>Software Testing</code> · <code>Debugging</code><br>
      <code>Code Quality</code>
    </td>
    <td width="50%" valign="top">
      <strong>BACKEND & DATABASES</strong><br><br>
      <code>Node.js</code> · <code>Express.js</code> · <code>FastAPI</code><br>
      <code>PostgreSQL</code> · <code>SQL Server</code> · <code>SQL</code><br>
      <code>Relational Database Design</code><br>
      <code>Database Indexing</code>
    </td>
  </tr>
  <tr>
    <td colspan="2" valign="top">
      <strong>SYSTEMS & DEVELOPER TOOLS</strong><br><br>
      <code>WebSockets</code> · <code>Socket.IO</code> · <code>Git</code> · <code>Docker</code> · <code>AWS</code>
    </td>
  </tr>
</table>

---

## `~/` how I ship software

<div align="center">

| 01 · UNDERSTAND | 02 · DESIGN | 03 · BUILD |
|:---:|:---:|:---:|
| Requirements & edge cases | Data models & APIs | Clean implementation |
| **04 · VERIFY** | **05 · HARDEN** | **06 · SHIP** |
| Unit & integration tests | Debugging & review | Deployment & monitoring |

</div>

```text
REQUIREMENTS
    ↓
PROBLEM DECOMPOSITION
    ↓
DATA STRUCTURES + ALGORITHMS
    ↓
DESIGN + IMPLEMENTATION
    ↓
TEST + DEBUG + REVIEW
    ↓
DEPLOY + OBSERVE + IMPROVE
```

---

## `~/` selected systems

| PROJECT | ENGINEERING FOCUS |
|---|---|
| [CodeTogether](https://github.com/deekshitaa1/CodeTogether) | Real-time collaborative coding, application architecture and communication |
| [ATLAS-X](https://github.com/deekshitaa1/ATLAS-X) | Storage engine concepts, indexing, transactions and distributed-storage research |
| [SQL Data Warehouse](https://github.com/deekshitaa1/sql-data-warehouse-project) | SQL engineering, ETL and dimensional data modelling |

---

## `~/` engineering principles

```text
01  CLARIFY THE REQUIREMENTS
02  THINK THROUGH EDGE CASES
03  PICK THE RIGHT DATA STRUCTURES
04  KEEP INTERFACES AND MODULES CLEAR
05  TEST FAILURE PATHS, NOT JUST HAPPY PATHS
06  DEBUG WITH EVIDENCE
07  REVIEW FOR CORRECTNESS AND MAINTAINABILITY
08  SHIP, MONITOR, LEARN, REPEAT
```

---

<div align="center">

### SOFTWARE DEVELOPMENT · BACKEND ENGINEERING · SYSTEM DESIGN

**Deekshita Rajesh**

[LinkedIn](https://www.linkedin.com/in/deekshita-rajesh) · [GitHub](https://github.com/deekshitaa1) · [Portfolio](https://deekshita-portfolio-one.vercel.app/)

<sub>`01010011 01000100 01000101` — STILL DEBUGGING. STILL BUILDING.</sub>

</div>
'''
md=os.path.join(base,"README-from-whoami-to-end.md")
with open(md,"w",encoding="utf-8") as f:f.write(readme)
zip_path="/mnt/data/sde_snake_ladder_blush_wine_readme.zip"
with zipfile.ZipFile(zip_path,"w",zipfile.ZIP_DEFLATED) as z:
    z.write(gif,"assets/sde-snake-ladder.gif")
    z.write(md,"README-from-whoami-to-end.md")
print("Created:",zip_path,os.path.getsize(zip_path))
print("GIF:",gif,os.path.getsize(gif))
print("Markdown:",md)


