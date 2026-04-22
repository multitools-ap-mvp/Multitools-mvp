File 1: index.html (The Core UI & Logic)
This file contains the HTML structure, the "CSS styling, and the JavaScript to handle the interactive menu and typing-effect banner.


File 2: manifest.json (PWA Manifest)
This file tells the browser that your app is installable, allows it to run in a standalone window, and gives it a mobile/desktop app icon.

{
  "name": "Apex Multi Tool DashBoard",
  "short_name": "ApexDash",
  "description": "A hacker multi-tool dashboard for development & PennTest setups.",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#050505",
  "theme_color": "#00ff41",
  "icons": [
    {
      "src": "https://via.placeholder.com/192x192.png?text=Apex",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "https://via.placeholder.com/512x512.png?text=Apex",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
(Note: I used placeholder icons to ensure it works instantly, will replace with Logo)

File 3: sw.js (Service Worker)
This file allows your dashboard to cache its assets so it loads instantly in the future and works entirely offline.

const CACHE_NAME = 'apex-dashboard-v1';
const urlsToCache = [
  './',
  './index.html',
  './manifest.json'
];

// Install Service Worker and Cache Files
self.addEventListener('install', event => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => {
        return cache.addAll(urlsToCache);
      })
  );
});

// Serve Cached files when offline
self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(response => {
        // Return cache or fetch from network
        return response || fetch(event.request);
      })
  );
});
How to use and extend this:
Test it Locally: PWAs require a local server to register Service Workers properly (due to security policies, opening the file directly via file:/// usually blocks the service worker).
If you have Python installed, open your terminal in the folder and type: python -m http.server 8000 (or python3).
If you have Node.js, you can run npx serve.
Open your browser and go to http://localhost:8000. You'll see an "Install App" icon pop up in the URL bar (in Chrome/Edge).
Extending the Menu:
To add a new tab (like "Database"), just copy an existing <div class="menu-item" data-target="database">...</div> in the nav section.
Then create a matching <div id="database" class="section">...</div> in the main section. The JavaScript automatically maps the data-target to the id!

 The CSS utilizes variable-based glowing shadow effects, so you can change --neon-green to #00ffff (Cyan) if you want a different cyberpunk aesthetic.


################################################################################################
Part 2
################################################################################################

