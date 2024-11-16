---
layout: post
title:  "How to use Colemak and Korean for Linux"
date:   2024-11-16 09:20:00 +0900
categories: linux korean
summary: Find out how to seamlessly use Colemak and Korean in Linux.
---

## Instructions

This assumes you have installed the following:
- localectl
- fcitx5 and fcitx5-hangul
- fcitx5-configtool

This also assumes that you have set the necessary environment variables to properly use
fcitx5. You can check this by running `fcitx5-diagnose` in the terminal.

1. Run the following command:

```
localectl set-x11-keymap us pc104 colemak korean:ralt_hangul,korean:rctrl_hanja
```

This assumes that you have a standard keyboard layout with a Right Alt and Right
Control key.

Then, logout and login again.

1. Open fcitx5-configtool. This can be done by right-clicking the fcitx system
tray icon and clicking "Configure" or running `fcitx5-configtool`.

1. In the Default Input Method group, set "Keyboard - English (US) - English
(Colemak)" as the first Input Method, and set Hangul as the second Input Method.

1. With Hangul selected, click on the Select Layout button (the button below the
gears, with the letter 'a'). Set the Layout to "English (US)" and the Variant to
"Default".

1. In the "Global Options" tab, click on Trigger Input Method. Add the "Hangul"
key by clicking on the + button on the right and pressing the Hangul key or the
Right Alt key.

1. Click OK to save your fcitx5 settings.

### Notes

This has been tested on Xfce and SwayWM in Arch Linux, so it should work on both
X and Wayland. However, keyboard layout settings set by localectl can be
overriden by certain DEs like GNOME or KDE, so consult your DE's manual to
properly set the Right Alt key and the Right Control key as the Hangul and Hanja
key respectively. Also, getting fcitx5 to work under GNOME has been a PITA from
experience, but YMMV.

## Some Info

I am in a somewhat unique position of being a Korean who uses Colemak for typing
English instead of QWERTY. The upshot is that my English typing has become more
comfortable; however, compatibility with Korean wasn't great until March 2024,
where I had to employ various hacks to make Korean usable with Colemak. Granted,
the [`kime`](https://github.com/Riey/kime) project was available, but it was
unstable and crashed Inkscape.

Fortunately, fcitx5-hangul now has an option to choose the reference layout as
QWERTY when fcitx5 is running in hangul mode. This matters because the way
Korean typing works is that it takes the English letter that was pressed and
converts it to a Hangul jamo. For example, the letter F in QWERTY corresponds to
the Hangul character ㄹ in Dubeolsik, the default Korean layout, so when fcitx
detects that the letter F has been pressed, the character ㄹ is displayed. This
starts to break down with non-QWERTY English layouts like Colemak. For example,
the key for F in QWERTY is T in Colemak, so fcitx would see the English
character T and output ㅅ, which is not what we want. We want our QWERTY
F/Colemak T key to output ㄹ.

Since fcitx5-hangul has an option to change the reference layout to QWERTY, we
can type in Colemak for English and switch to Korean Dubeolsik without any
hiccups. Shortcuts work properly as well, since the base keyboard layout is not
affected. And so, Colemak users can type in Korean and switch seamlessly between
the two.
