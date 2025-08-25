---
title: "Debugging Your Localhost App on an iPhone (2025 Edition)"
date: 2025-08-25
draft: false
tags: ["debugging", "react", "ios", "ngrok", "weinre", "mobile"]
categories: ["Web Development", "Frontend", "ngrok"]

authors:
  - admin
# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
image:
  filename: "ngrok.webp"
  focal_point: "center"
---

When you’re building a React (or any web) application, testing it on mobile devices is crucial. Desktop browser DevTools are great, but sometimes bugs only show up on **real devices**, with real screen sizes, Safari quirks, or iOS-specific CSS behaviors.

Back in 2019, I wrote about [how to debug localhost on mobile devices](https://medium.com/@mauricioasoto/debugando-qualquer-dispositivo-no-seu-local-host-3050ec943e91). A few years later, the tooling has improved, and we now have additional techniques like **ngrok tunnels** to simplify mobile debugging.

This article is the updated, 2025 edition. Let’s go step by step.

---

## 1. Debugging iPhone via Localhost

### Step 1 — Make localhost accessible on the iPhone

By default, `localhost` points only to your development machine. To reach it from your iPhone:

1. Ensure your iPhone and computer are on the **same Wi-Fi network**.
2. Find your computer’s local IP address.

   - On macOS/Linux:
     ```bash
     ifconfig | grep inet
     ```
   - On Windows:
     ```bash
     ipconfig
     ```

   You’ll see something like `192.168.0.102`.

3. Run your React app so it listens on `0.0.0.0` instead of `127.0.0.1`.

   For example, with Vite:

   ```bash
   npm run dev -- --host
   ```

or with CRA:

```bash
HOST=0.0.0.0 npm start
```

4. On your iPhone Safari or Chrome, open `http://192.168.0.102:3000`.

Now you’re serving localhost to your phone.

---

### Step 2 — Use Safari Web Inspector

If you have a Mac, the best way to debug is with **Safari’s remote DevTools**.

1. On the iPhone, enable **Settings → Safari → Advanced → Web Inspector**.
2. On your Mac Safari, go to **Preferences → Advanced → check “Show Develop menu in menu bar”**.
3. Connect the iPhone via USB.
4. In Safari (Mac), go to **Develop → \[Your iPhone] → \[The page you opened]**.

You now have full DevTools: inspect elements, tweak CSS, debug console logs, and analyze network requests directly from the iPhone’s Safari engine.

---

### Step 3 — Alternatives Without a Mac

If you don’t own a Mac, debugging iOS can be trickier. A few workarounds:

- **Eruda**: a mini DevTools injected into your page.

  ```js
  import eruda from "eruda";
  if (process.env.NODE_ENV === "development") {
    eruda.init();
  }
  ```

  This gives you a console and element inspector inside Safari on the iPhone itself.

- **Remote consoles**: You can log to services like LogRocket, Sentry, or even a simple websocket-based logger.

- **Chrome device mode**: While not identical to real iOS rendering, Chrome’s responsive design mode can help simulate issues quickly.

---

## 2. Debugging via ngrok (When Localhost Won’t Work)

Sometimes, your iPhone cannot access your local IP — maybe you’re on different networks, behind firewalls, or working remotely. That’s where **ngrok** comes in.

### What is ngrok?

[ngrok](https://ngrok.com) creates a **secure tunnel** from a public URL to your localhost. This means your iPhone (or anyone else) can access your app from anywhere, no network hacks required.

---

### Step 1 — Install and authenticate

1. Sign up for a free account at ngrok.com and copy your **authtoken**.
2. Install ngrok:

   ```bash
   brew install ngrok/ngrok/ngrok   # macOS
   choco install ngrok              # Windows
   ```

3. Authenticate:

   ```bash
   ngrok config add-authtoken <YOUR_TOKEN>
   ```

---

### Step 2 — Expose your app

If your React app runs on port 3000:

```bash
ngrok http 3000
```

You’ll get a public URL like:

```
https://abc123.ngrok.io
```

Open that URL on your iPhone’s Safari, and your local app loads instantly.

---

### Step 3 — Debug with Inspector

- Open `http://localhost:4040` on your computer to see the **ngrok inspector**.
  This shows incoming requests, headers, and responses. You can even replay requests — perfect for debugging APIs and webhooks.

- Combine this with **Safari Web Inspector** (as described earlier) to debug CSS, layout, and JavaScript issues on your iPhone while serving the app via ngrok.

---

### Notes & Best Practices

- **Ephemeral URLs**: Free ngrok URLs change on each run. For stable domains, use the paid plan.
- **OAuth callbacks**: If your app uses Auth0 or similar, add your ngrok URL to the allowed callback list.
- **Security**: ngrok exposes your local app to the internet. Use authentication or restrict access if sensitive data is involved.

---

## 3. Conclusion

Debugging on real devices is essential, and iOS can be especially tricky. You now have two reliable workflows:

- **Localhost + Safari Inspector** → Best when your Mac and iPhone are on the same network.
- **ngrok tunneling** → Best when localhost is unreachable, or when you want to share your app with teammates and clients.

Start with the localhost approach. If that fails, fire up ngrok and debug without friction.

**Happy debugging 🚀**
