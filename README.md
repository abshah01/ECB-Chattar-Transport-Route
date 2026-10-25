# Route Bus Tracker

Free, static website (GitHub + Vercel) with a free Firebase backend.
Students open the site with no login. Admin and captain log in with an ID and password.

## Step 1: Create the Firebase project (free)
1. Go to https://console.firebase.google.com and create a project (turn off Analytics).
2. **Build > Realtime Database > Create database.** Pick a location (Singapore is closest). Start in **locked mode**.
3. Open the **Rules** tab, paste the contents of `database.rules.json`, press **Publish**.
4. **Build > Authentication > Get started > Sign-in method > Email/Password > Enable.**

## Step 2: Connect the website
1. **Project settings (gear icon) > General > Your apps > Web (`</>`)**. Register an app, any name.
2. Copy the config values into `firebase-config.js`. `databaseURL` is shown there. If not, copy it from the top of the Realtime Database page.

## Step 3: Create the logins
In **Authentication > Users > Add user**, create:
- Email `admin@busroute.local`, password of your choice. Login ID is `admin`.
- Email `captain@busroute.local`, password of your choice. Login ID is `captain`. (The captain is the student with a smartphone who shares the bus location. The admin login can also share location.)

(You type only `admin` or `captain` on the site. The `@busroute.local` part is added automatically.)

Now give them roles. Copy each user's **User UID** from the Users table. Then open **Realtime Database > Data** and add:

```
roles
  <ADMIN_UID>:  admin
  <CAPTAIN_UID>: captain
```
(Click the + next to the root, name `roles`, add a child with the UID as the name and the text as the value.)

## Step 4: Put it on GitHub and Vercel
1. Create a GitHub repository and upload all these files (`index.html`, `firebase-config.js`, `database.rules.json`, `logo.png`, `README.md`).
2. Go to https://vercel.com, **Add New > Project**, import the repo, click **Deploy**. No build settings are needed.
3. Your site is live at `your-project.vercel.app`.

## Step 5: First use
1. Open the site, tap **Login**, sign in as `admin`.
2. Open the **Admin** tab: add the route name, stops, trips, contacts, Facebook link, notice. Press **Save**.
3. Your avatar: replace `logo.png` in the GitHub repo. Vercel redeploys automatically.

## Daily use by the captain
The captain opens the site on his smartphone, logs in as `captain`, opens the **Captain** tab, picks the trip and taps **Start sharing location**. Keep the screen on and the phone charging. Tap **Stop & end trip** at the end.

## Notes
- The Firebase API keys in `firebase-config.js` are meant to be public. Security comes from the database rules.
- The free Firebase plan is far more than a single bus route needs.
- Change a password any time in Firebase **Authentication > Users**.

## Home page and map
- The home page has a hero banner, a "departure in" card, a live map with the bus, and the stop timeline.
- The map uses OpenStreetMap through Leaflet. It is free and needs no key.
- For the route line to appear, each stop needs latitude and longitude. In **Admin**, stand at the stop and press **use my location**, or type the coordinates.
- Admin can also change the big headline text (Tagline).
