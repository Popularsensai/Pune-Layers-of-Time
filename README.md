# Pune-Layers-of-Time
A museum experience controlled via phone, capable of projecting output on bigger screens

**Instructions for running the experience**
# Pune: Layers of Time (local, reliable pairing)

## Run (needs Node.js 18+)
    npm install
    npm start

1. Open **http://localhost:3000** on the laptop. A QR code and a 4-letter code appear.
2. Put the phone on the **same Wi-Fi** and scan the QR with the camera app.
3. First time only: the phone warns about the certificate (it is self-signed for your laptop's IP). Tap
   Advanced -> Proceed (Android) or Show Details -> visit this website (iOS). HTTPS is what unlocks motion sensors.
4. On the phone tap **Calibrate** (iOS asks for motion permission), point at the target, then point and tap.

No QR scan possible? On the phone open `https://<laptop-ip>:3443/p` and type the code.

## Photos
On first start the server downloads one open-licensed photo per location from Wikimedia Commons into `public/img`
(needs internet on the laptop; takes about a minute, progress prints in the terminal). Credit and licence appear
on every photo frame. Until a photo arrives, the frame says "loading"; refresh the page afterwards.
- Wrong or missing photo? Open `media.json`, pin an exact Commons file: `"lal-mahal":{"file":"Lal_Mahal_Pune.jpg", ...}`,
  delete that file's entry from `public/img/index.json`, and run `npm run photos`.
- Only CC BY, CC BY-SA, CC0 and public-domain photos are accepted. Non-commercial/no-derivative licences are skipped.
- Check each photo and caption with the curator before any public installation.

## If it does not connect
- Same Wi-Fi? Guest/"client isolation" networks block phone-to-laptop traffic. Use a hotspot from the phone or laptop instead.
- Firewall: allow Node.js on ports 3000 and 3443.
- Wrong IP in the QR (VPN or several adapters): `LAN_IP=192.168.1.20 npm start`
- Certificate or sensors still blocked: run a tunnel (e.g. `npx localtunnel --port 3000`) and start with
  `PUBLIC_URL=https://<tunnel-url> npm start`. The QR then uses that trusted HTTPS address.
- Motion unavailable? The phone switches to a touchpad automatically (drag to aim, tap to select).

## Test pairing logic
    npm test
