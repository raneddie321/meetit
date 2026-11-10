# Meet It

A video calling app inspired by Zoom and Google Meet. The whole app is one `index.html` file that uses the [Agora RTC Web SDK](https://www.agora.io/) for real-time audio and video.

- **Create a meeting:** you get a random 6-digit code, a share dialog (copy the code or an invite link), and you join the room as the **host**.
- **Join with a code:** enter your name and the 6-digit code your friend shared.
- Responsive video grid for 1, 2 or many people, with name tags, a host badge, mute indicators and a highlight on whoever is talking.
- Mic and camera toggles (also `Ctrl/⌘+D` and `Ctrl/⌘+E`), a copy-invite button, a call timer, and a participant count.
- Leave cleanly: tracks are stopped, the camera light turns off, and the connection is closed.

## 1. Get an Agora App ID (free, about 2 minutes)

Agora doesn't provide a shared public App ID. Every App ID belongs to one account.

1. Sign up at <https://console.agora.io>.
2. Create a project and pick **Testing mode: APP ID** (no App Certificate). Meet It joins without tokens, so a project with an App Certificate won't work unless you add a token server.
3. Copy the 32-character App ID.

Then do **one** of these:

- **Hard-code it (recommended):** open `index.html`, find `const AGORA_APP_ID = "";` and paste your ID between the quotes.
- **Set it at runtime:** leave the constant empty. Open the deployed site, expand **Connection settings** on the lobby, and paste the App ID. It's saved in your browser and added to invite links, so friends who open your link connect automatically.

## 2. Deploy to Vercel

Meet It is a static site with no build step.

**From GitHub:** go to <https://vercel.com/new>, import this repository, keep the defaults (Framework Preset: *Other*, no build command, output directory = root), then click **Deploy**.

**From the CLI:**

```bash
npx vercel --prod
```

Vercel serves over HTTPS, which browsers require before they allow camera and microphone access.

## 3. Run locally

Camera and microphone access needs `https://` or `localhost`:

```bash
npx serve .
```

Then open <http://localhost:3000>. To try a two-person call, open the site in two browser windows (or on a phone and a laptop), create a meeting in one, and join with the code in the other.

## Files

| File          | Purpose                                                          |
|---------------|------------------------------------------------------------------|
| `index.html`  | The entire app: HTML layout, CSS styling, JavaScript and the Agora integration |
| `vercel.json` | Static hosting config: clean URLs, plus headers that allow camera and mic access |
