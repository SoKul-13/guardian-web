# Connect Google to Guardian

About 10 minutes, once. You create your own Google "app" so Guardian talks to Google directly
from your computer. No company sits in the middle, and nothing is shared with anyone.

**What you get:** Calendar, Tasks, unread Gmail and recent Drive files in your morning briefing,
an Agenda card on Today, schedule and email search in Ask, and an "Export to Google Sheets" button
for your workouts and journal.

**Access:** read-only for Calendar, Tasks, Gmail and Drive. Guardian can only write to the one
spreadsheet it creates ("Guardian Log"). Email is summarized by the local model on your computer.

---

## Step 1: Create a Google Cloud project (free)

1. Go to **https://console.cloud.google.com** and sign in with the Google account you want to connect.
2. If asked, accept the terms. No billing or credit card is needed.
3. Click the **project picker** at the top left → **New project**.
4. Name it `Guardian` → **Create**. Make sure it's selected in the project picker afterwards.

## Step 2: Turn on the five APIs

1. Open **https://console.cloud.google.com/apis/library** (menu → APIs & Services → Library).
2. Search for each of these, open it, and click **Enable**:
   - **Google Calendar API**
   - **Google Tasks API**
   - **Gmail API**
   - **Google Drive API**
   - **Google Sheets API**

## Step 3: Set up the sign-in screen

1. Open **https://console.cloud.google.com/auth/overview** (menu → APIs & Services → OAuth consent screen,
   which Google now calls **Google Auth Platform**). Click **Get started**.
2. **App information:** App name `Guardian`, and your email as the support email → **Next**.
3. **Audience:** choose **External** → **Next**.
4. **Contact information:** your email → **Next** → agree to the policy → **Create**.
5. In the left menu open **Audience**:
   - Under **Test users**, click **Add users**, enter your own Gmail address, **Save**.
   - Then click **Publish app** → **Confirm**.
     *This matters:* apps left in "Testing" get signed out by Google every 7 days.
     Publishing your own private app is fine; it just shows an "unverified app" warning when you
     connect (step 6), because Google hasn't reviewed it. Nobody else can use it without your file.

## Step 4: Create the Desktop client and download it

1. In the left menu open **Clients** → **Create client**.
2. **Application type:** `Desktop app`. **Name:** `Guardian Desktop` → **Create**.
3. In the dialog, click **Download JSON**. Save the file (it looks like `client_secret_….json`).
   Keep it private. It identifies your app.

## Step 5: Add it to Guardian

1. Open Guardian on your computer → **Settings** → **Google**.
2. Click **Choose file** and select the JSON file you downloaded. You'll see "✓ Client added."
3. Click **Connect Google**.

## Step 6: Approve in your browser

1. Your browser opens Google's sign-in page. Choose your account.
2. You'll see **"Google hasn't verified this app."** This is expected for your own app.
   Click **Advanced** → **Go to Guardian (unsafe)**.
3. Tick the permissions (Calendar, Tasks, Gmail, Drive) → **Continue**.
4. The page says **"Guardian is connected to Google."** Close the tab.

Settings → Google now shows "Connected as you@gmail.com".

## Step 7: Check it works

- **Today → Run briefing now.** You should get *Schedule & tasks*, *Inbox* and *Drive activity*
  sections, and an **Agenda** card with today's events.
- **Ask:** "What's on my calendar tomorrow?" or "Search my email for messages from my professor this week".
- **Settings → Google → Export workouts + journal to Google Sheets** creates "Guardian Log" in your Drive.
- Optional: set `google.export_after_briefing: true` in Settings to refresh that sheet every morning.

---

## Troubleshooting

| You see | Fix |
|---|---|
| `access_denied` or "app is being tested" | Add your Gmail under **Audience → Test users**, or publish the app (step 3.5). |
| `Google 403 … has not been used in project` | That API isn't enabled. Do step 2 for the API named in the message, wait a minute, run the briefing again. |
| "Google sign-in expired. Reconnect…" | The app was left in Testing (7-day limit). Publish it (step 3.5), then Settings → Google → Connect again. |
| "That is not a Google OAuth client file" | You downloaded the wrong file. Create a **Desktop app** client (step 4) and download its JSON. |
| Browser didn't open | Guardian is waiting for 5 minutes. Click Connect again. |
| Want to disconnect | Settings → Google → **Disconnect**. This also revokes the token at Google. You can also remove access at https://myaccount.google.com/permissions |

## Where things are stored

- `~/Guardian/secrets/google-client.json`: your Desktop client (from step 4)
- `~/Guardian/secrets/google-token.json`: the sign-in token, renewed automatically

The `secrets` folder is never included in the GitHub backup. On the phone you see your calendar and
mail summaries through your computer. The phone never holds Google access itself.
