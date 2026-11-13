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

---



import math, os, zipfile
from PIL import Image, ImageDraw, ImageFilter, ImageFont
import numpy as np

outdir = "/mnt/data/sde_3d_radar_assets"
os.makedirs(outdir, exist_ok=True)

W, H = 900, 620
FRAMES = 48
FONT_PATH = "/usr/share/fonts/truetype/dejavu/DejaVuSans.ttf"
FONT_BOLD = "/usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf"
def font(size, bold=False):
    return ImageFont.truetype(FONT_BOLD if bold else FONT_PATH, size)

def glow_circle(layer, xy, r, color, blur=18):
    glow = Image.new("RGBA", layer.size, (0,0,0,0))
    gd = ImageDraw.Draw(glow)
    gd.ellipse((xy[0]-r, xy[1]-r, xy[0]+r, xy[1]+r), fill=color)
    glow = glow.filter(ImageFilter.GaussianBlur(blur))
    layer.alpha_composite(glow)
    d = ImageDraw.Draw(layer)
    d.ellipse((xy[0]-r*0.48, xy[1]-r*0.48, xy[0]+r*0.48, xy[1]+r*0.48), fill=color)

def make_engineering():
    frames=[]
    cx, cy = 450, 330
    for f in range(FRAMES):
        im=Image.new("RGBA",(W,H),(5,12,18,255))
        # subtle ambient glow
        bg=Image.new("RGBA",(W,H),(0,0,0,0))
        bd=ImageDraw.Draw(bg)
        bd.ellipse((120,35,780,610),fill=(0,170,140,28))
        bg=bg.filter(ImageFilter.GaussianBlur(90)); im.alpha_composite(bg)
        d=ImageDraw.Draw(im)
        # header / micro labels
        d.text((48,34),"ENGINEERING SYSTEMS",font=font(17,True),fill=(95,255,204,255))
        d.text((48,62),"PROBLEM SOLVING  /  DESIGN  /  IMPLEMENTATION",font=font(11),fill=(133,164,171,255))
        d.text((48,555),"LIVE MODEL  •  STRUCTURE  •  REASONING",font=font(11,True),fill=(95,255,204,230))
        d.text((690,555),"01 / 02",font=font(12,True),fill=(133,164,171,255))
        # perspective ellipse grid, horizontal rings
        for k in range(1,7):
            rx=45+k*47
            ry=rx*0.43
            d.ellipse((cx-rx,cy-ry,cx+rx,cy+ry),outline=(27,105,105,150),width=2)
        # radial spokes
        for a in range(0,360,30):
            rad=math.radians(a)
            x=cx+330*math.cos(rad); y=cy+142*math.sin(rad)
            d.line((cx,cy,x,y),fill=(24,83,91,130),width=1)
        # base disk and concentric layered rims
        d.ellipse((cx-300,cy-128,cx+300,cy+128),outline=(37,255,190,100),width=3)
        d.arc((cx-310,cy-133,cx+310,cy+133),180,355,fill=(58,255,204,220),width=4)
        d.arc((cx-310,cy-133,cx+310,cy+133),5,175,fill=(31,119,121,180),width=3)
        # central 3D core
        for z in range(7):
            yoff=z*7
            d.ellipse((cx-75,cy-34+yoff,cx+75,cy+34+yoff),outline=(30,190,155,110),width=2)
        d.ellipse((cx-75,cy-34,cx+75,cy+34),fill=(9,40,43,255),outline=(98,255,204,255),width=3)
        d.text((cx-37,cy-12),"CORE",font=font(19,True),fill=(177,255,227,255))
        # rotating scan wedge
        angle=math.radians(f*360/FRAMES)
        sweep=Image.new("RGBA",(W,H),(0,0,0,0))
        sd=ImageDraw.Draw(sweep)
        pts=[(cx,cy)]
        for t in np.linspace(0,1,30):
            a=angle+t*0.18
            pts.append((cx+300*math.cos(a),cy+128*math.sin(a)))
        pts.append((cx,cy))
        sd.polygon(pts,fill=(0,255,175,28))
        sd.line((cx,cy,cx+300*math.cos(angle),cy+128*math.sin(angle)),fill=(92,255,205,220),width=3)
        sweep=sweep.filter(ImageFilter.GaussianBlur(2)); im.alpha_composite(sweep)
        # orbiting nodes with labels
        nodes=[("DSA",0.0),("OOP",1.05),("API",2.12),("DBMS",3.18),("DESIGN",4.23),("CONCURRENCY",5.28)]
        for idx,(label,base) in enumerate(nodes):
            a=base+angle*0.23
            x=cx+225*math.cos(a); y=cy+96*math.sin(a)
            glow_circle(im,(int(x),int(y)),14,(38,255,184,180),20)
            d=ImageDraw.Draw(im)
            d.text((x-30,y-32),label,font=font(11,True),fill=(195,255,235,255))
        # depth rails and HUD details
        d=ImageDraw.Draw(im)
        d.line((145,470,755,470),fill=(22,90,92,130),width=1)
        for x in range(145,756,30):
            d.line((x,466,x,474),fill=(45,145,128,150),width=1)
        d.rounded_rectangle((48,112,240,145),radius=8,outline=(35,150,132,160),width=1)
        d.text((62,121),"01  /  ENGINEERING",font=font(12,True),fill=(148,255,219,255))
        frames.append(im.convert("RGB"))
    return frames

def make_delivery():
    frames=[]
    cx,cy=450,320
    stages=["TEST","BUILD","DEPLOY","OBSERVE","IMPROVE"]
    for f in range(FRAMES):
        im=Image.new("RGBA",(W,H),(5,12,18,255))
        bg=Image.new("RGBA",(W,H),(0,0,0,0)); bd=ImageDraw.Draw(bg)
        bd.ellipse((100,60,820,580),fill=(0,125,180,24))
        bg=bg.filter(ImageFilter.GaussianBlur(95)); im.alpha_composite(bg)
        d=ImageDraw.Draw(im)
        d.text((48,34),"DELIVERY & RELIABILITY",font=font(17,True),fill=(98,210,255,255))
        d.text((48,62),"TESTING  /  DEPLOYMENT  /  MONITORING",font=font(11),fill=(133,164,171,255))
        d.text((48,555),"CONTINUOUS DELIVERY  •  FEEDBACK  •  RESILIENCE",font=font(11,True),fill=(98,210,255,230))
        d.text((690,555),"02 / 02",font=font(12,True),fill=(133,164,171,255))
        # isometric platform
        top=[(120,285),(450,145),(780,285),(450,430)]
        d.polygon(top,fill=(10,31,43,255),outline=(58,190,225,190))
        d.line(top+[top[0]],fill=(58,190,225,190),width=2)
        # grid on platform
        for t in np.linspace(0.12,0.88,7):
            x1=120+(450-120)*t; y1=285+(145-285)*t
            x2=450+(780-450)*t; y2=145+(285-145)*t
            d.line((x1,y1,x2,y2),fill=(25,91,112,100),width=1)
            xa=120+(450-120)*t; ya=285+(430-285)*t
            xb=450+(780-450)*t; yb=145+(285-145)*t
            d.line((xa,ya,xb,yb),fill=(25,91,112,100),width=1)
        # pipeline nodes
        positions=[(190,280),(320,225),(450,280),(580,225),(710,280)]
        pulse=(math.sin(f*2*math.pi/FRAMES)+1)/2
        for i,((x,y),label) in enumerate(zip(positions,stages)):
            # 3D pillar
            h=58+int(12*math.sin(f*2*math.pi/FRAMES+i*.8))
            d.polygon([(x-34,y),(x,y-17),(x+34,y),(x,y+17)],fill=(13,77,91,255),outline=(80,220,240,220))
            d.polygon([(x-34,y),(x,y+17),(x,y+17+h),(x-34,y+h)],fill=(7,43,58,255),outline=(45,145,170,180))
            d.polygon([(x,y+17),(x+34,y),(x+34,y+h),(x,y+17+h)],fill=(9,57,73,255),outline=(45,145,170,180))
            glow_circle(im,(x,y-4),int(11+4*pulse),(45,210,255,160),18)
            d=ImageDraw.Draw(im)
            box=d.textbbox((0,0),label,font=font(11,True)); tw=box[2]-box[0]
            d.text((x-tw/2,y+h+25),label,font=font(11,True),fill=(193,241,250,255))
        # moving data packet along pipeline
        progress=(f/FRAMES)*4
        seg=min(3,int(progress)); frac=progress-seg
        x1,y1=positions[seg]; x2,y2=positions[seg+1]
        px=x1+(x2-x1)*frac; py=y1+(y2-y1)*frac-5
        glow_circle(im,(int(px),int(py)),17,(70,225,255,200),24)
        d=ImageDraw.Draw(im)
        d.rounded_rectangle((48,112,248,145),radius=8,outline=(45,155,190,160),width=1)
        d.text((62,121),"02  /  RELIABILITY",font=font(12,True),fill=(157,232,255,255))
        # side instrumentation
        d.rounded_rectangle((690,110,850,174),radius=9,outline=(37,120,148,160),width=1)
        d.text((706,122),"PIPELINE",font=font(10,True),fill=(120,210,235,255))
        d.text((706,143),"HEALTH  :  NOMINAL",font=font(9),fill=(110,240,190,255))
        frames.append(im.convert("RGB"))
    return frames

eng=make_engineering()
rel=make_delivery()
eng_path=os.path.join(outdir,"engineering-3d.gif")
rel_path=os.path.join(outdir,"delivery-reliability-3d.gif")
eng[0].save(eng_path,save_all=True,append_images=eng[1:],duration=90,loop=0,optimize=True)
rel[0].save(rel_path,save_all=True,append_images=rel[1:],duration=90,loop=0,optimize=True)

readme_section = r'''<!-- Keep everything above this point unchanged: profile header + ~/ whoami -->

---

## `~/` engineering systems

<div align="center">
  <img src="assets/engineering-3d.gif" width="49%" alt="Animated 3D engineering systems radar">
  <img src="assets/delivery-reliability-3d.gif" width="49%" alt="Animated 3D software delivery and reliability pipeline">
</div>

<p align="center">
  <sub>ENGINEERING FUNDAMENTALS · DELIVERY · RELIABILITY</sub>
</p>

---

## `~/` engineering loop

| 01 · DEFINE | 02 · DESIGN | 03 · BUILD |
|---|---|---|
| Requirements, constraints, edge cases | APIs, data models, architecture | Modular implementation, code review |
| 04 · VERIFY | 05 · OPERATE | 06 · IMPROVE |
| Unit and integration tests | Deployment, observability, reliability | Profiling, debugging, optimization |

<p align="center"><em>Correctness first. Design for change. Operate with confidence.</em></p>
'''
section_path=os.path.join(outdir,"README-section.md")
with open(section_path,"w",encoding="utf-8") as f: f.write(readme_section)

zip_path="/mnt/data/sde_3d_animated_assets.zip"
with zipfile.ZipFile(zip_path,"w",zipfile.ZIP_DEFLATED) as z:
    z.write(eng_path,"assets/engineering-3d.gif")
    z.write(rel_path,"assets/delivery-reliability-3d.gif")
    z.write(section_path,"README-section.md")

print("Created:")
print(eng_path, os.path.getsize(eng_path))
print(rel_path, os.path.getsize(rel_path))
print(section_path)
print(zip_path, os.path.getsize(zip_path))

