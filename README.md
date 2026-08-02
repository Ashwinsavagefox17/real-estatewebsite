# Premium Real Estate Experience

A cinematic, award-winning digital experience for luxury real estate. This project uses advanced web technologies to deliver an immersive, butter-smooth, 4K 60FPS video-scrubbing experience linked directly to the user's scroll wheel.

Built with a focus on high-end motion design, performance, and luxury aesthetics, the site bypasses traditional CDN streaming limitations by loading massive high-bitrate video files directly into memory, accompanied by a dynamic, real-time GSAP loading sequence.

## 🚀 Live Demo

- **Netlify Deployment:** [https://realestateez.netlify.app/](https://realestateez.netlify.app/)
- **Vercel Deployment:** [https://real-estatewebsite-seven.vercel.app/](https://real-estatewebsite-seven.vercel.app/)

## ✨ Key Features

- **Scroll-Bound Video Scrubbing:** The core of the experience. A 116MB, 4K 60FPS architectural time-lapse is perfectly synchronized to the user's scroll position, allowing them to manually "scrub" time forwards and backwards through the construction and walkthrough of a luxury villa.
- **Cinematic GSAP Preloader:** A custom-built, agency-grade preloader using GSAP. It features a luxury minimalist design (inspired by top-tier production agencies), ambient animated noise, and a real-time percentage counter that tracks the exact byte-for-byte download progress of the massive video payload.
- **Advanced Memory Buffering:** To prevent the video from stalling or throwing `401 Unauthorized` CDN timeouts from rapid HTTP range-requests, the site utilizes the `fetch()` API and ReadableStreams to download the entire video into a local memory Blob before playback begins. 
- **Lenis Smooth Scrolling:** Physical scroll wheels and trackpads are intercepted and smoothed using the Lenis physics engine (`lerp: 0.2`). This gives the page a heavy, momentum-driven luxury feel similar to native mobile applications.
- **Split-Text Typography Reveals:** Utilizing `SplitType` and GSAP, hero typography is broken into individual lines and beautifully staggered upward upon load completion.
- **Responsive Fluid Typography:** CSS `clamp()` functions ensure that the luxury typography scales perfectly across ultra-wide monitors, laptops, and mobile devices without arbitrary breakpoints.

## 🛠️ Technology Stack

- **Core:** HTML5, Vanilla JavaScript, Vanilla CSS (CSS Variables & Clamp)
- **Animation Engine:** GSAP (GreenSock) Core + CustomEase
- **Text Manipulation:** SplitType
- **Scroll Physics:** Lenis (@studio-freight/lenis)
- **Asset Pipeline:** Git LFS (Large File Storage) for handling the 116MB 4K source video (`scrub_lv.mp4`).

## ⚙️ How It Works (The Technical Magic)

Creating a smooth scroll-scrub experience with a 100MB+ video on free hosting tiers (Vercel/Netlify) is notoriously difficult because CDNs will throttle or kill the connection when a user rapidly scrolls and fires off hundreds of HTTP Range Requests per second. 

**The Solution:**
1. **The Blob Fetch:** The site intercepts the `<video>` source and runs a manual `fetch()` request. 
2. **The Stream Reader:** We attach a `ReadableStream` to the fetch response to calculate the exact `Content-Length` and chunks downloaded.
3. **The GSAP Proxy:** We feed this exact byte-math into a GSAP proxy object, which tweens the percentage text from `0%` to `100%` with buttery smoothness.
4. **The Blob Swap:** Once fully downloaded, the chunks are converted into a `Blob`, a local `ObjectURL` is created, and it is injected instantly into the `<video src="...">` tag.
5. **The Lenis Sync:** Finally, `requestAnimationFrame` calculates the physical distance scrolled, applies the Lenis easing mathematics, and snaps the `video.currentTime` to match the exact frame of the video.

## 💻 Local Development

1. Clone the repository:
   ```bash
   git clone https://github.com/Ashwinsavagefox17/real-estatewebsite.git
   ```
2. Because the project uses Git LFS for the massive 4K video, ensure you have LFS installed and pull the media:
   ```bash
   git lfs install
   git lfs pull
   ```
3. Start a local server (do not open the HTML file directly in the browser due to CORS/Fetch restrictions):
   ```bash
   python -m http.server 8000
   ```
   *Or use Live Server in VS Code.*
4. Open `http://localhost:8000` in your browser.

## 🎨 Design Inspiration
The loader and typography treatments were heavily inspired by high-end digital production agencies (such as `donprod.uk`), utilizing pure blacks, stark whites, tabular numerals, and premium easing curves (`expo.out`, `power4.inOut`).
