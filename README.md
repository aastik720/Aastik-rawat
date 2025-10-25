#!/usr/bin/env python3
"""
add_logo.py - Overlay a logo onto a portrait image.

Usage examples:
  python add_logo.py \
    --portrait "aastik rawat portfolio picture.jpg" \
    --logo "logo.png" \
    --out "assets/portrait-with-logo.png" \
    --position southeast \
    --scale 20 \
    --padding 10 \
    --opacity 90

Options:
  --portrait  PATH   Path to the portrait image (required)
  --logo      PATH   Path to the logo image (required)
  --out       PATH   Output path (default: portrait-with-logo.png)
  --position POS    Position: southeast, southwest, northeast, northwest, center (default: southeast)
  --scale     NUM    Logo size as percentage of portrait width (e.g. 20) or fraction (0.2). Default 20 (means 20%).
  --padding   NUM    Padding in pixels from the chosen corner (default 10)
  --opacity   NUM    Logo opacity 0-100 (default 100)
"""
import argparse
import os
from PIL import Image, ImageEnhance

def parse_scale(value):
    v = float(value)
    # if greater than 1, interpret as percent (e.g. 20 -> 0.2)
    if v > 1:
        return v / 100.0
    return v  # already a fraction

def overlay_logo(portrait_path, logo_path, out_path,
                 position="southeast", scale=0.2, padding=10, opacity=100):
    # Open portrait
    portrait = Image.open(portrait_path).convert("RGBA")
    pw, ph = portrait.size

    # Open logo
    logo = Image.open(logo_path).convert("RGBA")
    lw, lh = logo.size

    # Resize logo to scale * portrait width (preserve aspect ratio)
    target_width = int(pw * scale)
    if target_width <= 0:
        raise ValueError("Computed target logo width <= 0. Check scale value.")
    # Compute new height keeping aspect ratio
    aspect = lh / lw
    new_size = (target_width, max(1, int(target_width * aspect)))
    logo = logo.resize(new_size, Image.LANCZOS)
    lw, lh = logo.size

    # Apply opacity if needed
    if opacity < 100:
        # Split alpha, modify it
        alpha = logo.split()[3]
        alpha = ImageEnhance.Brightness(alpha).enhance(opacity / 100.0)
        logo.putalpha(alpha)

    # Compute position
    pos = (0, 0)
    pos_name = position.lower()
    if pos_name in ("southeast", "se"):
        pos = (pw - lw - padding, ph - lh - padding)
    elif pos_name in ("southwest", "sw"):
        pos = (padding, ph - lh - padding)
    elif pos_name in ("northeast", "ne"):
        pos = (pw - lw - padding, padding)
    elif pos_name in ("northwest", "nw"):
        pos = (padding, padding)
    elif pos_name in ("center", "middle", "c"):
        pos = ((pw - lw) // 2, (ph - lh) // 2)
    else:
        raise ValueError(f"Unknown position: {position}")

    # Create a new image with portrait and paste logo with alpha as mask
    composed = Image.new("RGBA", portrait.size)
    composed.paste(portrait, (0, 0))
    composed.paste(logo, pos, logo)

    # If output extension is JPEG, convert to RGB and save as JPEG (no alpha)
    out_ext = os.path.splitext(out_path)[1].lower()
    if out_ext in (".jpg", ".jpeg"):
        composed_rgb = composed.convert("RGB")
        composed_rgb.save(out_path, quality=90)
    else:
        # PNG or other formats keep RGBA
        composed.save(out_path)

    print(f"Saved composed image to: {out_path}")

def main():
    parser = argparse.ArgumentParser(description="Overlay a logo onto a portrait image.")
    parser.add_argument("--portrait", required=True, help="Path to portrait image")
    parser.add_argument("--logo", required=True, help="Path to logo image (PNG recommended for transparency)")
    parser.add_argument("--out", default="portrait-with-logo.png", help="Output path")
    parser.add_argument("--position", default="southeast",
                        choices=["southeast","se","southwest","sw","northeast","ne","northwest","nw","center","middle","c"],
                        help="Position for logo (default: southeast)")
    parser.add_argument("--scale", type=float, default=20.0, help="Logo size as percentage (e.g. 20) or fraction (0.2). Default 20")
    parser.add_argument("--padding", type=int, default=10, help="Padding from edge in pixels (default 10)")
    parser.add_argument("--opacity", type=int, default=100, help="Opacity 0-100 (default 100)")
    args = parser.parse_args()

    scale = parse_scale(args.scale)
    if not (0 < scale <= 1):
        raise ValueError("Scale must be a fraction between 0 and 1 (or percentage >0), e.g. 20 or 0.2")

    if not (0 <= args.opacity <= 100):
        raise ValueError("Opacity must be between 0 and 100")

    overlay_logo(args.portrait, args.logo, args.out, args.position, scale, args.padding, args.opacity)

if __name__ == "__main__":
    main()<h1 align="center">Hi 👋, I'm AASTIK RAWAT</h1>
!logo (aastik rawat portfolio picture.jpg)
<h3 align="center">A passionate Full-stack Dev | Linux & Security | AI Innovator |  Networking | Problem Solver | Ethical Hacking | Innovation Seeker | Lifelong Learner” from India from India</h3>

<p align="left"> <img src="https://komarev.com/ghpvc/?username=aastik720&label=Profile%20views&color=0e75b6&style=flat" alt="aastik720" /> </p>

<p align="left"> <a href="https://github.com/ryo-ma/github-profile-trophy"><img src="https://github-profile-trophy.vercel.app/?username=aastik720" alt="aastik720" /></a> </p>

- 🔭 I’m currently working on ["RUDRA"](ON GOING)

- 🌱 I’m currently learning **python,c++,java script,rust,dart**

- 👯 I’m looking to collaborate on ["REGEL"](ON GOING)

- 🤝 I’m looking for help with ["FITVISION AI"](ON GOING)

- 👨‍💻 All of my projects are available at [on buliding](on buliding)

- 💬 Ask me about **coding,hacking,**

- 📫 How to reach me **rawataastik729@gmail.com**

- 📄 Know about my experiences [on building](on building)

- ⚡ Fun fact **i am mad to achieve my fucking goal**

<h3 align="left">Connect with me:</h3>
<p align="left">
<a href="https://twitter.com/pending" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/twitter.svg" alt="pending" height="30" width="40" /></a>
<a href="https://linkedin.com/in/pending" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg" alt="pending" height="30" width="40" /></a>
<a href="https://fb.com/pending" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/facebook.svg" alt="pending" height="30" width="40" /></a>
<a href="https://instagram.com/pending" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/instagram.svg" alt="pending" height="30" width="40" /></a>
<a href="https://www.youtube.com/c/pending" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/youtube.svg" alt="pending" height="30" width="40" /></a>
<a href="https://www.hackerrank.com/pending" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/hackerrank.svg" alt="pending" height="30" width="40" /></a>
<a href="https://www.leetcode.com/pending" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/leet-code.svg" alt="pending" height="30" width="40" /></a>
<a href="https://discord.gg/pending" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/discord.svg" alt="pending" height="30" width="40" /></a>
</p>

<h3 align="left">Languages and Tools:</h3>
<p align="left"> <a href="https://developer.android.com" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/android/android-original-wordmark.svg" alt="android" width="40" height="40"/> </a> <a href="https://aws.amazon.com" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" alt="aws" width="40" height="40"/> </a> <a href="https://www.gnu.org/software/bash/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/gnu_bash/gnu_bash-icon.svg" alt="bash" width="40" height="40"/> </a> <a href="https://www.cprogramming.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/c/c-original.svg" alt="c" width="40" height="40"/> </a> <a href="https://www.w3schools.com/cpp/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/cplusplus/cplusplus-original.svg" alt="cplusplus" width="40" height="40"/> </a> <a href="https://dart.dev" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/dartlang/dartlang-icon.svg" alt="dart" width="40" height="40"/> </a> <a href="https://firebase.google.com/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/firebase/firebase-icon.svg" alt="firebase" width="40" height="40"/> </a> <a href="https://flask.palletsprojects.com/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/pocoo_flask/pocoo_flask-icon.svg" alt="flask" width="40" height="40"/> </a> <a href="https://flutter.dev" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/flutterio/flutterio-icon.svg" alt="flutter" width="40" height="40"/> </a> <a href="https://git-scm.com/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" alt="git" width="40" height="40"/> </a> <a href="https://www.w3.org/html/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg" alt="html5" width="40" height="40"/> </a> <a href="https://www.java.com" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" alt="java" width="40" height="40"/> </a> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" alt="javascript" width="40" height="40"/> </a> <a href="https://www.linux.org/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/linux/linux-original.svg" alt="linux" width="40" height="40"/> </a> <a href="https://www.mongodb.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mongodb/mongodb-original-wordmark.svg" alt="mongodb" width="40" height="40"/> </a> <a href="https://www.mysql.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original-wordmark.svg" alt="mysql" width="40" height="40"/> </a> <a href="https://www.photoshop.com/en" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/photoshop/photoshop-line.svg" alt="photoshop" width="40" height="40"/> </a> <a href="https://www.php.net" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/php/php-original.svg" alt="php" width="40" height="40"/> </a> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a> <a href="https://pytorch.org/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/pytorch/pytorch-icon.svg" alt="pytorch" width="40" height="40"/> </a> <a href="https://www.rust-lang.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/rust/rust-plain.svg" alt="rust" width="40" height="40"/> </a> <a href="https://www.sketch.com/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/sketchapp/sketchapp-icon.svg" alt="sketch" width="40" height="40"/> </a> <a href="https://www.tensorflow.org" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/tensorflow/tensorflow-icon.svg" alt="tensorflow" width="40" height="40"/> </a> </p>

<p><img align="center" src="https://github-readme-stats.vercel.app/api/top-langs?username=aastik720&show_icons=true&locale=en&layout=compact" alt="aastik720" /></p>

<p><img align="center" src="https://github-readme-streak-stats.herokuapp.com/?user=aastik720&" alt="aastik720" /></p>

