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


from PIL import Image, ImageDraw, ImageFont, ImageFilter
import os, math, zipfile

root = "/mnt/data/sde_snake_ladder_blush_wine"
assets = os.path.join(root, "assets")
os.makedirs(assets, exist_ok=True)

W, H, FRAMES = 1000, 620, 48
REG = "/usr/share/fonts/truetype/dejavu/DejaVuSans.ttf"
BOLD = "/usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf"
def font(size, bold=False):
    return ImageFont.truetype(BOLD if bold else REG, size)

def glow(im, x, y, radius, color, blur=18):
    layer = Image.new("RGBA", im.size, (0, 0, 0, 0))
    ImageDraw.Draw(layer).ellipse((x-radius, y-radius, x+radius, y+radius), fill=color)
    im.alpha_composite(layer.filter(ImageFilter.GaussianBlur(blur)))

frames = []
for frame in range(FRAMES):
    im = Image.new("RGBA", (W, H), (24, 14, 21, 255))
    haze = Image.new("RGBA", (W, H), (0, 0, 0, 0))
    hd = ImageDraw.Draw(haze)
    hd.ellipse((80, 55, 930, 600), fill=(174, 73, 111, 34))
    hd.ellipse((280, 80, 780, 530), fill=(216, 164, 119, 22))
    im.alpha_composite(haze.filter(ImageFilter.GaussianBlur(95)))
    d = ImageDraw.Draw(im)

    d.text((42, 26), "THE SDE CLIMB", font=font(23, True), fill=(255, 222, 233, 255))
    d.text((44, 60), "A CAREER BOARD GAME, EXCEPT THE BUGS MOVE FIRST", font=font(11, True), fill=(218, 177, 190, 255))

    # Board frame and 60 serpentine squares
    x0, y0, cw, ch = 188, 128, 78, 62
    d.rounded_rectangle((x0-13, y0-13, x0+10*cw+13, y0+6*ch+13),
                        radius=20, fill=(48, 25, 37, 255),
                        outline=(203, 139, 157, 230), width=3)
    for row in range(6):
        for col in range(10):
            x, y = x0 + col*cw, y0 + row*ch
            num = row*10 + (col+1) if row % 2 == 0 else row*10 + (10-col)
            fill = (91, 48, 65, 255) if (row+col) % 2 == 0 else (113, 63, 79, 255)
            d.rounded_rectangle((x+2, y+2, x+cw-2, y+ch-2), radius=6,
                                fill=fill, outline=(173, 117, 137, 180), width=1)
            d.text((x+8, y+6), f"{num:02d}", font=font(10, True), fill=(246, 220, 227, 230))

    # Ladders with champagne rails and rungs
    def ladder(p1, p2):
        x1, y1 = p1; x2, y2 = p2
        d.line((x1-8, y1, x2-8, y2), fill=(240, 202, 148, 255), width=5)
        d.line((x1+8, y1, x2+8, y2), fill=(240, 202, 148, 255), width=5)
        for t in [k/8 for k in range(1, 8)]:
            x, y = x1+(x2-x1)*t, y1+(y2-y1)*t
            d.line((x-9, y, x+9, y), fill=(255, 235, 197, 255), width=3)
    ladder((x0+1.5*cw, y0+5.3*ch), (x0+4.0*cw, y0+2.0*ch))
    ladder((x0+6.0*cw, y0+4.6*ch), (x0+8.0*cw, y0+1.2*ch))

    # Curved snake, with a small moving tongue/head glow
    snake_pts = []
    for k in range(100):
        t = k/99
        x = x0 + cw*(8.85 - 5.9*t)
        y = y0 + ch*(0.65 + 4.55*t) + math.sin(t*math.pi*4 + frame*2*math.pi/FRAMES)*5
        snake_pts.append((x, y))
    d.line(snake_pts, fill=(116, 43, 70, 255), width=17, joint="curve")
    d.line(snake_pts, fill=(237, 145, 174, 255), width=8, joint="curve")
    hx, hy = snake_pts[0]
    glow(im, int(hx), int(hy), 20, (255, 164, 193, 140), 20)
    d = ImageDraw.Draw(im)
    d.ellipse((hx-13, hy-13, hx+13, hy+13), fill=(248, 177, 198, 255),
              outline=(255, 237, 239, 255), width=2)
    d.ellipse((hx-5, hy-4, hx-2, hy-1), fill=(70, 25, 43, 255))
    d.ellipse((hx+3, hy-4, hx+6, hy-1), fill=(70, 25, 43, 255))
    d.line((hx+1, hy+5, hx+12, hy+10), fill=(255, 220, 224, 255), width=2)

    # Animated gold player token advances along the board
    progress = frame/(FRAMES-1)*59
    row = int(progress)//10
    col = int(progress)%10
    if row % 2:
        col = 9-col
    px, py = int(x0+(col+.5)*cw), int(y0+(row+.5)*ch)
    glow(im, px, py, 21, (255, 220, 160, 150), 20)
    d = ImageDraw.Draw(im)
    d.ellipse((px-10, py-10, px+10, py+10), fill=(255, 225, 176, 255),
              outline=(255, 249, 225, 255), width=2)

    # Side console
    d.rounded_rectangle((35, 145, 164, 515), radius=15,
                        fill=(48, 27, 38, 245), outline=(176, 111, 137, 190), width=1)
    d.text((53, 169), "PLAYER", font=font(10, True), fill=(224, 177, 194, 255))
    d.text((53, 193), "SDE", font=font(24, True), fill=(255, 230, 237, 255))
    d.line((53, 238, 145, 238), fill=(173, 111, 137, 180), width=1)
    d.text((53, 260), "XP", font=font(10, True), fill=(224, 177, 194, 255))
    d.text((53, 282), f"{int(progress*17):03d}", font=font(23, True), fill=(255, 230, 237, 255))
    d.text((53, 340), "BUGS", font=font(10, True), fill=(224, 177, 194, 255))
    d.text((53, 362), "∞", font=font(26, True), fill=(255, 206, 187, 255))
    d.text((53, 425), "EXPECTED", font=font(8, True), fill=(201, 162, 177, 255))
    d.text((53, 440), "BEHAVIOUR", font=font(8, True), fill=(201, 162, 177, 255))

    # Bottom caption
    d.rounded_rectangle((x0, 535, 970, 590), radius=12,
                        fill=(48, 27, 38, 245), outline=(194, 132, 151, 160), width=1)
    d.text((x0+17, 554), "LADDER: TESTS PASS  →  DEPLOY", font=font(12, True), fill=(255, 226, 233, 255))
    d.text((690, 555), "SNAKE: WORKS ON MY MACHINE", font=font(10, True), fill=(255, 199, 178, 255))
    frames.append(im.convert("RGB"))

gif_path = os.path.join(assets, "sde-snake-ladder.gif")
frames[0].save(gif_path, save_all=True, append_images=frames[1:], duration=100, loop=0, optimize=True)

readme = r'''<!--
REPLACE ONLY FROM THIS `~/ whoami` SECTION TO THE END OF README.md.
DO NOT change the profile photo, typing banner, social links, or anything above this comment.
This is GitHub README Markdown + supported inline HTML. It is NOT Python or CSS.
-->

---

## `~/` whoami

```console
$ whoami
Deekshita Rajesh

$ role --target
Software Development Engineer

$ engineering --focus
Data Structures & Algorithms · Backend Systems · System Design

$ objective
Build correct, maintainable software. Understand the trade-offs. Ship with confidence.
```

I enjoy solving engineering problems from first principles: selecting appropriate data structures, designing clear interfaces, building dependable backend services, and testing how systems behave beyond the happy path.

> **Good code gets it working. Good engineering makes it dependable.**

---

## `~/` the SDE climb

<div align="center">
  <img src="assets/sde-snake-ladder.gif" width="100%" alt="Animated blush pink, chocolate and wine-red SDE snake and ladder board">
  <br>
  <sub>ROLL THE DICE · SOLVE THE BUG · CLIMB THE LADDER · SHIP THE BUILD</sub>
</div>

<table>
  <tr>
    <td width="50%" valign="top">
      <strong>THE LADDER — LEVEL UP</strong><br><br>
      <code>DSA</code> → <code>OOP</code> → <code>Design</code> → <code>Implementation</code> → <code>Testing</code> → <code>Deployment</code>
    </td>
    <td width="50%" valign="top">
      <strong>THE SNAKES — REAL-WORLD SURPRISES</strong><br><br>
      <code>Off-by-one errors</code> · <code>Race conditions</code> · <code>Failed tests</code> · <code>Slow queries</code> · <code>Unexpected input</code>
    </td>
  </tr>
</table>

<p align="center">
  <sub>Every bug is a lesson. Every passing test is one step up. The snake has read the production logs.</sub>
</p>

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

<table>
  <tr>
    <td align="center" width="33%"><sub>01</sub><br><strong>UNDERSTAND</strong><br>Requirements & edge cases</td>
    <td align="center" width="33%"><sub>02</sub><br><strong>DESIGN</strong><br>Data models & APIs</td>
    <td align="center" width="33%"><sub>03</sub><br><strong>BUILD</strong><br>Clean implementation</td>
  </tr>
  <tr>
    <td align="center"><sub>04</sub><br><strong>VERIFY</strong><br>Unit & integration tests</td>
    <td align="center"><sub>05</sub><br><strong>HARDEN</strong><br>Debugging & review</td>
    <td align="center"><sub>06</sub><br><strong>SHIP</strong><br>Deploy & monitor</td>
  </tr>
</table>

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
| [CodeTogether](https://github.com/deekshitaa1/CodeTogether) | Real-time collaborative coding, backend integration and application architecture |
| [ATLAS-X](https://github.com/deekshitaa1/ATLAS-X) | Storage-engine concepts, indexing, transactions and distributed-storage research |
| [SQL Data Warehouse](https://github.com/deekshitaa1/sql-data-warehouse-project) | SQL engineering, ETL and dimensional data modelling |

---

## `~/` engineering principles

```text
01  CLARIFY REQUIREMENTS BEFORE IMPLEMENTING
02  REASON ABOUT EDGE CASES AND FAILURE MODES
03  CHOOSE DATA STRUCTURES DELIBERATELY
04  KEEP MODULES AND INTERFACES CLEAR
05  TEST FAILURE PATHS, NOT ONLY HAPPY PATHS
06  DEBUG WITH EVIDENCE
07  REVIEW FOR CORRECTNESS AND MAINTAINABILITY
08  SHIP · MONITOR · LEARN · IMPROVE
```

---

<div align="center">

### SOFTWARE DEVELOPMENT · BACKEND ENGINEERING · SYSTEM DESIGN

**Deekshita Rajesh**

[LinkedIn](https://www.linkedin.com/in/deekshita-rajesh) · [GitHub](https://github.com/deekshitaa1) · [Portfolio](https://deekshita-portfolio-one.vercel.app/)

<sub>`01010011 01000100 01000101` — STILL DEBUGGING. STILL BUILDING.</sub>

</div>
'''
md_path = os.path.join(root, "README-from-whoami-to-end.md")
with open(md_path, "w", encoding="utf-8") as f:
    f.write(readme)

zip_path = "/mnt/data/sde_snake_ladder_blush_wine_readme.zip"
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    z.write(gif_path, "assets/sde-snake-ladder.gif")
    z.write(md_path, "README-from-whoami-to-end.md")

print("Created files:")
print(gif_path, os.path.getsize(gif_path))
print(md_path, os.path.getsize(md_path))
print(zip_path, os.path.getsize(zip_path))


