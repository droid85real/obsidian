css roadmap: https://youtu.be/aLzfFJb8rWo
ui/ux design guide: https://youtu.be/wIuVvCuiJhU



---
CSS stands for Cascade Style Sheet

Three ways to add CSS to HTML

Inline 


---
Font size
Title 32px
Body 18px
Small 14px

---
**Tweening**
short for "in-betweening," is the digital process of generating intermediate frames between two keyframes to create smooth, automated motion. 

###### GSAP
gsap playlist: https://www.youtube.com/playlist?list=PLbtI3_MArDOnIIJxB6xFtpnhM0wTwz0x6

01:  https://youtu.be/9C03V1dXxOU?list=PLbtI3_MArDOnIIJxB6xFtpnhM0wTwz0x6
Gsap basic, 
tween { to , from, fromto }
inside tween { delay, duration, rotate, repeat, yoyo (back and forth) }

stagger: Delays each target’s animation by a set interval, creating a sequential (one-after-another) motion effect instead of all elements animating at once.

timeline: Sequence controller that lets you chain multiple animations with precise timing, overlaps, and relative positions.


02: https://youtu.be/aezzM70lWDo?list=PLbtI3_MArDOnIIJxB6xFtpnhM0wTwz0x6
ScrollTrigger { trigger, scroller, markers, start, end, scrub, pin}
scrub : Scrub makes the animation progress follow the scrollbar position (scroll)
Without scrub:  
Scroll reaches the trigger → animation plays like a normal timeline (time-based, independent of further scrolling).

pin : Pin freezes an element in place while the scroll continues.
Used for:
• sticky sections  
• horizontal scroll illusions  
• storytelling panels  
• parallax layouts


03: https://youtu.be/asdNfZfHT34?list=PLbtI3_MArDOnIIJxB6xFtpnhM0wTwz0x6
svg animate, gsap easing (control speed)

04: https://youtu.be/Ziv1G994SrM?list=PLbtI3_MArDOnIIJxB6xFtpnhM0wTwz0x6
Custom Cursor Animation ,dets, 


---
###### gsap in react 
docs: https://gsap.com/resources/React/
lib: https://www.npmjs.com/package/@gsap/react
https://youtu.be/AW1yfBKRMKc?t=411

`npm i @gsap/react gsap react-responsive`

need to register plugin at the global. To makes the plugin available to GSAP animations
`gsap.registerPlugin(ScrollTrigger, SplitText);`

useGSAP 

https://youtu.be/l0aI8Ecumy8?t=141
earlier gsap.content for cleanups because useEffect are unreliable and can be unpredictive but now useGSAP instead

scoping instead of drowning in useRefs.
Without `scope`, GSAP will query the whole document.  
With `scope`, it only touches elements inside that component.

dependency and revertOnUpdate

context: https://youtu.be/l0aI8Ecumy8?t=490
it tells about stored tween in useGSAP 

contextSafe


gsapstagger: https://youtu.be/AW1yfBKRMKc?t=1070

scrollTrigger: https://youtu.be/AW1yfBKRMKc?t=1300

GSAP text: https://youtu.be/AW1yfBKRMKc?t=1706

gsap project: https://youtu.be/AW1yfBKRMKc?t=1862

fixed choppy video scroll .video smoothing using ffmpeg https://youtu.be/AW1yfBKRMKc?t=5011 
download ffmpeg: https://www.ffmpeg.org/download.html
`ffmpeg -i input.mp4 -vf scale=960 :- 1 -movflags faststart -vcodec libx264 -crf 20 -g 1 -pix_fmt yuv420p output.mp4`



---

**useGSAP**
- React hook from GSAP that runs animations in a scoped, lifecycle-safe way (auto cleanup, no stale refs, no duplicate runs in StrictMode).

- GSAP hook that works like useLayoutEffect but adds automatic scoping, cleanup, and StrictMode-safe animation handling.


