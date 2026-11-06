# Motion Recipes (GSAP — ไม่ผูก framework)

## Parallax layer
```js
gsap.to(el, {
  yPercent: speed * -20,        // speed: 0.2 ช้า … 1 เร็ว
  ease: 'none',
  scrollTrigger: { trigger: section, start: 'top bottom', end: 'bottom top', scrub: true },
})
```

## Reveal (fade-up)
```js
gsap.from(items, {
  y: 24, opacity: 0, duration: 0.8, stagger: 0.08, ease: 'power2.out',
  scrollTrigger: { trigger: section, start: 'top 80%' },
})
```

## Timeline line draw
```js
gsap.fromTo(line, { scaleY: 0 }, {
  scaleY: 1, transformOrigin: 'top', ease: 'none',
  scrollTrigger: { trigger: list, start: 'top 70%', end: 'bottom 60%', scrub: true },
})
```

## Card tilt (pointer: fine เท่านั้น)
```js
const qx = gsap.quickTo(card, 'rotateY', { duration: 0.4 })
const qy = gsap.quickTo(card, 'rotateX', { duration: 0.4 })
card.addEventListener('pointermove', e => {
  const r = card.getBoundingClientRect()
  qx(((e.clientX - r.left) / r.width - 0.5) * 10)
  qy(-((e.clientY - r.top) / r.height - 0.5) * 10)
})
```

## Lenis + ScrollTrigger
```js
const lenis = new Lenis()
lenis.on('scroll', ScrollTrigger.update)
gsap.ticker.add(t => lenis.raf(t * 1000))
gsap.ticker.lagSmoothing(0)
```
