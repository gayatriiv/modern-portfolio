# portfolio website

a modern, interactive portfolio website built with smooth scroll animations and dynamic interactions using advanced web technologies.

## overview

this portfolio showcases project work and personal information with smooth scrolling effects, animated text reveals, and interactive hover states. the website uses locomotive scroll for smooth scrolling behavior and gsap (greensock animation platform) for timeline-based animations.

## technical architecture

### core technologies

- **locomotive scroll**: provides smooth scrolling with momentum and scroll detection across the entire viewport
- **gsap (greensock animation platform)**: handles all animations including timeline-based sequences and scroll-triggered animations
- **vanilla javascript**: manages event listeners, mouse tracking, and animation orchestration
- **css3**: styling with flexbox, transforms, and transitions for responsive design

### key features

#### 1. smooth scrolling

locomotive scroll instance initialized on the main element enables momentum-based smooth scrolling instead of default browser behavior and provides scroll event detection for triggering animations.

#### 2. hero section animations

the hero section features a staggered text reveal animation that triggers on page load:

- navigation slides in from top with opacity animation
- heading text elements translate up from bottom with stagger effect
- hero footer fades in after heading animation
- uses gsap timeline for sequenced animations with precise timing
- total sequence duration: 2.5 seconds with Expo.easeInOut easing

#### 3. mouse tracking circle

an interactive mini circle follows the mouse cursor with scale transformations:

- tracks mouse position in real-time
- scales based on mouse movement velocity
- stretches horizontally when moving fast, vertically when moving slow
- creates organic fluid motion effect using gsap transformations
- updates with 100ms throttle for performance optimization

#### 4. project hover interactions

when hovering over project elements:

- project images fade in to full opacity
- image follows mouse position within the element
- image rotates based on horizontal mouse movement velocity
- rotation clamped between -20 to 20 degrees for smooth effect
- image hides when mouse leaves the element

#### 5. scroll triggers

scroll trigger configuration available for future implementations:

- can be used to trigger animations at specific scroll positions
- enables element animations as they enter viewport
- works in conjunction with locomotive scroll for precise timing

## file structure

```
portfolio/
├── index.html          # main html structure
├── style.css           # primary styling and layout
├── loco.css            # locomotive scroll styles
├── script.js           # animation logic and interactions
├── README.md           # project documentation
└── assets/             # images and media files
    ├── momos.jpg
    ├── plug.png
    └── [other project images]
```

## code breakdown

### html structure

- **hero section**: navigation, main heading with bounding elements, small headings, footer links
- **second section**: project showcase with three portfolio items
- **about section**: circular profile image with text content
- **subscribe section**: call-to-action for youtube channel
- **footer**: copyright and social links

### css styling

bounding elements use overflow hidden containers for reveal animations. initial state moves text 100% down for animation reveal using transform translateY. absolute positioning enables mini circle tracking. flexbox layout provides responsive alignment throughout.

key classes:

- `.bounding`: container with overflow hidden for text reveal
- `.boundingelem`: text elements with initial translateY(100%)
- `.elem`: project items with relative positioning and flex layout
- `#minicircle`: absolute positioned tracking element

### javascript architecture

#### locomotive scroll initialization

```javascript
const scroll = new LocomotiveScroll({
  el: document.querySelector("#main"),
  smooth: true,
});
```

enables smooth scrolling behavior with momentum and scroll event detection.

#### first page animation timeline

`firstPageAnim()` function creates gsap timeline:

- animates navigation in from top (duration: 1.5s)
- reveals bounding elements with stagger effect (0.2s between each)
- brings hero footer in simultaneously (duration: 1.5s)
- uses Expo.easeInOut easing for smooth acceleration

#### mouse tracking system

`circleChaptaKaro()` and `circleMouseFollower()` functions:

- capture mouse position on every move event
- calculate velocity by comparing current and previous coordinates
- clamp scale values between 0.8 and 1.2
- apply scale transformations to mini circle via gsap
- throttle updates with 100ms delay for performance

#### project interactions

event listeners on each `.elem` element:

- mouseleave: fades out project image
- mousemove: updates image position and rotation based on cursor
- calculates image position relative to element
- applies rotation between -20 and 20 degrees based on velocity

## animation details

### gsap timeline sequences

hero section animations use gsap timeline for precise control:

- duration: 2.5 seconds total
- easing: Expo.easeInOut for smooth acceleration/deceleration
- stagger on bounding elements: 0.2 seconds between each
- overlapping animations create fluid sequence
- delay values overlap animations for continuous flow

### smooth scroll behavior

locomotive scroll manages all scroll events:

- smooth momentum scrolling on all browsers
- enables passive event listeners for performance
- provides scroll position data for future scroll triggers
- integrates with gsap scroll trigger for advanced animations

### transform animations

all movement uses css transforms for gpu acceleration:

- translate: position changes on mini circle and mouse movement
- scale: size transformations on hover and velocity tracking
- rotate: image rotation on project hover
- all applied via gsap for timeline control and easing

## interaction flow

### on page load

1. mini circle initializes at cursor position
2. hero animation timeline plays automatically
3. text reveals with staggered timing (0.2s intervals)
4. user can immediately interact with elements after animation

### on mouse move

1. mini circle follows cursor continuously
2. circle scales based on movement velocity
3. circle updates position at 100ms intervals
4. smooth scaling creates organic motion

### on project element hover

1. project image fades in (opacity 0 to 1)
2. image position follows precise mouse coordinates
3. image rotates based on horizontal velocity measurement
4. image smoothly hides when mouse leaves element

## performance considerations

- gpu acceleration through css transforms instead of position changes
- pointer-events: none on non-interactive images prevents event propagation
- debounced circle updates prevent excessive redraws
- locomotive scroll handles scroll optimization internally
- gsap timeline batches animations for efficiency
- passive event listeners improve scrolling performance

## browser compatibility

- modern browsers with es6 support required
- locomotive scroll requires modern scroll apis
- gsap compatible with all modern browsers
- css3 features widely supported in current versions
- smooth scroll behavior supported in modern browsers

## future enhancements

- enable scroll trigger animations for scroll-based element reveals
- add parallax scrolling effects for visual depth
- implement lazy loading for project images
- add contact form with email functionality
- optimize for mobile responsive layouts
- add page transition animations
- implement keyboard navigation support
