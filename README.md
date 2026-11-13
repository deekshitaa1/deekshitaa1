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
import math, os, zipfile

outdir = "/mnt/data/amazon_sde_readme_pink"
os.makedirs(outdir, exist_ok=True)
W, H, N = 960, 560, 40
font_reg = "/usr/share/fonts/truetype/dejavu/DejaVuSans.ttf"
font_bold = "/usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf"
def F(sz, bold=False):
    return ImageFont.truetype(font_bold if bold else font_reg, sz)

def glow(base, x, y, r, color, blur=16):
    lay = Image.new("RGBA", base.size, (0,0,0,0))
    ImageDraw.Draw(lay).ellipse((x-r,y-r,x+r,y+r), fill=color)
    lay = lay.filter(ImageFilter.GaussianBlur(blur))
    base.alpha_composite(lay)
    ImageDraw.Draw(base).ellipse((x-r*.42,y-r*.42,x+r*.42,y+r*.42), fill=color)

frames=[]
cx, cy = 480, 290
for i in range(N):
    im = Image.new("RGBA", (W,H), (15,13,18,255))
    # soft rose/gold atmospheric bloom
    haze=Image.new("RGBA",(W,H),(0,0,0,0))
    hd=ImageDraw.Draw(haze)
    hd.ellipse((90,45,870,540), fill=(194,91,129,38))
    hd.ellipse((280,110,700,470), fill=(235,190,112,20))
    haze=haze.filter(ImageFilter.GaussianBlur(95)); im.alpha_composite(haze)
    d=ImageDraw.Draw(im)
    d.text((48,28),"ENGINEERING CAPABILITY MATRIX",font=F(16,True),fill=(255,220,232,255))
    d.text((48,54),"SOFTWARE DEVELOPMENT ENGINEER  /  SYSTEMS THINKING",font=F(10),fill=(194,177,185,255))
    d.rounded_rectangle((48,90,260,122),radius=9,fill=(54,34,45,230),outline=(211,133,160,170),width=1)
    d.text((62,99),"01  /  CORE ENGINEERING",font=F(11,True),fill=(255,221,232,255))
    # perspective radar platform
    for k in range(1,7):
        rx=44+k*48; ry=rx*.43
        d.ellipse((cx-rx,cy-ry,cx+rx,cy+ry),outline=(166,103,126,105),width=2)
    for a in range(0,360,30):
        aa=math.radians(a)
        d.line((cx,cy,cx+330*math.cos(aa),cy+142*math.sin(aa)),fill=(117,81,99,95),width=1)
    d.ellipse((cx-310,cy-134,cx+310,cy+134),outline=(242,196,132,210),width=3)
    d.arc((cx-318,cy-139,cx+318,cy+139),185,350,fill=(255,221,232,230),width=4)
    # stacked depth rings
    for z in range(1,7):
        d.ellipse((cx-90,cy-42+z*7,cx+90,cy+42+z*7),outline=(178,103,132,110),width=2)
    d.ellipse((cx-90,cy-42,cx+90,cy+42),fill=(64,36,49,255),outline=(255,220,232,255),width=3)
    d.text((cx-47,cy-13),"SDE CORE",font=F(18,True),fill=(255,242,224,255))
    # sweep wedge rotates
    ang=2*math.pi*i/N
    sweep=Image.new("RGBA",(W,H),(0,0,0,0)); sd=ImageDraw.Draw(sweep)
    pts=[(cx,cy)]
    for t in range(26):
        a=ang+t*.012
        pts.append((cx+310*math.cos(a),cy+134*math.sin(a)))
    pts.append((cx,cy))
    sd.polygon(pts,fill=(255,190,213,25))
    sd.line((cx,cy,cx+310*math.cos(ang),cy+134*math.sin(ang)),fill=(255,224,177,230),width=3)
    im.alpha_composite(sweep)
    # nodes
    nodes=[("DSA",0),("OOP",1.05),("API",2.1),("DATABASES",3.15),("DESIGN",4.2),("RELIABILITY",5.25)]
    for label, a0 in nodes:
        a=a0+ang*.16
        x=int(cx+238*math.cos(a)); y=int(cy+102*math.sin(a))
        glow(im,x,y,13,(255,190,213,190),18)
        ImageDraw.Draw(im).text((x-34,y-30),label,font=F(10,True),fill=(255,235,241,255))
    d=ImageDraw.Draw(im)
    # side telemetry panels
    d.rounded_rectangle((48,420,270,500),radius=12,fill=(36,25,33,210),outline=(174,112,139,150),width=1)
    d.text((66,438),"DESIGN PRINCIPLE",font=F(10,True),fill=(236,190,207,255))
    d.text((66,462),"Correctness  ·  Clarity",font=F(12),fill=(255,244,232,255))
    d.rounded_rectangle((690,420,912,500),radius=12,fill=(36,25,33,210),outline=(207,166,111,150),width=1)
    d.text((708,438),"ENGINEERING MODE",font=F(10,True),fill=(236,190,207,255))
    d.text((708,462),"Design  /  Build  /  Verify",font=F(11),fill=(255,244,232,255))
    d.text((48,530),"PINK  /  IVORY  /  CHAMPAGNE GOLD",font=F(9,True),fill=(195,168,180,255))
    d.text((840,530),"LIVE  •  01",font=F(9,True),fill=(237,204,160,255))
    frames.append(im.convert("RGB"))

gif_path=os.path.join(outdir,"sde-engineering-radar.gif")
frames[0].save(gif_path, save_all=True, append_images=frames[1:], duration=100, loop=0, optimize=True)

md = r'''<!-- SDE TECHNICAL SKILLS — place this AFTER ~/ whoami; keep the profile header and whoami unchanged -->

---

## `~/` technical skills

<div align="center">
  <img src="assets/sde-engineering-radar.gif" width="100%" alt="Animated software engineering capability radar">
</div>

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
      <code>Software Design</code><br>
      <code>Design Patterns</code><br>
      <code>Distributed Systems</code><br>
      <code>RESTful API Development</code><br>
      <code>Software Testing</code><br>
      <code>Debugging</code><br>
      <code>Code Quality</code>
    </td>
    <td width="50%" valign="top">
      <strong>BACKEND & DATABASES</strong><br><br>
      <code>Node.js</code> <code>Express.js</code><br>
      <code>FastAPI</code> <code>PostgreSQL</code><br>
      <code>SQL Server</code> <code>SQL</code><br>
      <code>Relational Database Design</code><br>
      <code>Database Indexing</code>
    </td>
  </tr>
  <tr>
    <td colspan="2" valign="top">
      <strong>SYSTEMS & DEVELOPER TOOLS</strong><br><br>
      <code>WebSockets</code> <code>Socket.IO</code>
      <code>Git</code> <code>Docker</code> <code>AWS</code>
    </td>
  </tr>
</table>

<p align="center">
  <sub>PROBLEM SOLVING · DESIGN · IMPLEMENTATION · TESTING · RELIABILITY</sub>
</p>
'''
md_path=os.path.join(outdir,"TECHNICAL-SKILLS-README.md")
with open(md_path,"w",encoding="utf-8") as f: f.write(md)
zip_path="/mnt/data/amazon_sde_pink_readme_package.zip"
with zipfile.ZipFile(zip_path,"w",zipfile.ZIP_DEFLATED) as z:
    z.write(gif_path,"assets/sde-engineering-radar.gif")
    z.write(md_path,"TECHNICAL-SKILLS-README.md")
print("Created", gif_path, os.path.getsize(gif_path), md_path, zip_path, os.path.getsize(zip_path))

print(zip_path, os.path.getsize(zip_path))

