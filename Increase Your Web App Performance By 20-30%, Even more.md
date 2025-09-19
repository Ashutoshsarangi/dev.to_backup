**Web Vitals**

1. FCP (First Contentful Paint) **(Response Quick)**
2. LCP (Largest Contentful Paint) **(get to the point)**
  Big Images/article
3. CLS (Cumulative layout Shift) **(Don't move Elements)**
4. First input Delay (**Don't load Too Much Data)**
  Brower in the background handling the Asyc works and because of that it puts delay 


**NOTE:-**

**Cumulative layout Shift**

1. The movement that impacts the page elements, in the entire lifetime of the document the user sees.
2. also, this is costly as the layout will change, and then it it do the Layout, paint, and composite again. Also post that if there are any damaged pixels it will re-render again




**Bench Marks**

LCP:

good < 2.5 sec < Need Improvement < 4.0 sec < Poor

FID:

good < 100 M.sec < Need Improvement < 300 M.sec < Poor

CLS:-

good < 0.1 sec < Need Improvement < 0.25 sec < Poor


**tools:- **

field data (Actual user data) for Application performance monitoring 

1. Light House (Local Performance Monitoring is specific depending on your system preferences)
2. https://developer.chrome.com/docs/crux/dashboard/
3. https://www.lightest.app/ (Compare with similar applications)
4. https://www.performancebudget.io/

**Improving on FCP:**

1. If your users are far away from the server better to use CDNS.
2. Its is the big impact (Can consider gzip as well)

**Improving LCP**

1. Defer resources until later (defer/ async in the script)
 

```html
<script src="/assets/js/abc.js" defer></script>
// For Other image tags / video links from I frame we can use intersection Observer to handle when the view port intersect with the element.

```
**2. Optimize images (Very Important)**
  As I mentioned above along with this even we load bit latter but some images are 2Mb size and which is not needed 

there are 2 approaches  

a. use image compressor (tinyPng) (imagemin npm package)
b. use kind of srcset for various responsive designs,as mentioned below

```html
<img
data-src="pic-1200.min.png"
src="" 
data-srcset=""
data-srcset="pic-600.png 600w, pic-900.png 900w, pic-1200.png 1200w"
sizes="(max-width: 600px) 600px, (max-width: 900px) 900px, 1200px"
/>
```

**3. reduce request Overhead**
 
preload and preconnect

```html
<link rel="preconnect" href="https://fonts.gstatic.com" />
<link rel="preload" href="/assets/css/index.css" />
<link rel="prefetch" href="/assets/css/index.css" />
```
**preload**

- preloads a resource in the background with high-priority

**prefetch**

- preloads and caches a resource in the background with low-priority

**preconnect:** 

- Establishes early connections to an external resource.

**Preconnects to a Resource:** 

- It sets up an early connection to a resource's origin (e.g., a third-party domain) before the resource is requested or fetched. This helps reduce latency.

**DNS Lookup, TLS, and TCP Handshake:** 

- When you use preconnect, the browser performs the DNS lookup, establishes a TCP connection, and negotiates TLS (if required) in advance. This means that when the resource is needed, these steps are already completed.

**Improving CLS**

1. Please don't move Elements , i.e thumb rule 
2. for Advertise we need to mention this is the max height with allocated **div**
3. Let's say the cookie banner we can fix ed at the bottom. Then there would be a major boost compared to we show them on top and when the user clicks accept and disappear our layout structure will not impacted
3. We can target for 0.01 (0.059) (CLS)(LightBox)
4. for image tags we can specify the **width and height attributes**

**Improving FID**
 
a. Don't defere everything to the end, because let's say your LCP is done and the user trying to interact with the UI but as we did everything **defer** the Browser till loading those on background so not a good Idea to all to defer.

Only not required immediately js files we can defer.

**Improvement 3 Sec in font-face**

```CSS
@font-face {
  src: 'font-url',
  font-display: 'auto'; // default
}

// Here Browser waits for 3 sec to load
```

```CSS
@font-face {
  src: 'font-url',
  font-display: 'fallback';
}

// render unstyled text immediately, 
//switch if font is loaded with in 3 secs.
```

```CSS
@font-face {
  src: 'font-url',
  font-display: 'optional';
}

// render unstyled text immediately, 
//switch only on refresh if its downloaded.
```

**Reference:-**
https://frontendmasters.com/courses/web-perf
