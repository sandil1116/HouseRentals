# Our Rentals

A simple website to look after 11 annexes and 3 houses (more can be added any time).

**What it does**

- Home page shows every annex and house in a colour: green = paid, red = not paid, orange = part paid, grey = empty.
- "Things to look at" box: empty places ready to rent, tenants who are leaving soon, who has not paid, money owed from earlier months, bills not made yet, complaints waiting.
- Light bill and water bill: type the new meter reading, the website takes the last reading from last month and calculates the bill (units used × rate + fixed charge). Rent and other charges are added to get the total.
- Mark a bill as PAID with one button, or save a part payment.
- Print a bill, or send it to the tenant on WhatsApp.
- Complaints: add them yourself, or tenants send them from the **/complain** page (no password). Tap "Fixed" when done.
- Tenants: add a new tenant, record the day they leave. From that day the place shows as EMPTY.
- **/available** page (no password) lists empty places with rent, to share with people looking for a place.
- Admin (admin password only): add new annexes or houses, change names, rent and rates, change the electricity or water rate for every place at once, hide places you no longer rent.

**Two passwords**

- `APP_PASSWORD` is for everyday use (bills, payments, complaints, tenants).
- `ADMIN_PASSWORD` can do all of that and also open the Admin page.

The first time the website opens it creates Annex 1–11 and House 1–3 automatically. Rename them and set rent and rates in Admin.

---

## Put it online for free (about 15 minutes)

You need three free accounts: GitHub, Neon (the database) and Vercel (the website).

### 1. Database (Neon, free)

1. Go to https://neon.tech and sign up.
2. Create a project (choose the region **Singapore**, it is closest to Sri Lanka).
3. On the dashboard click **Connect** and copy the connection string. It looks like
   `postgresql://user:password@ep-xxxx.ap-southeast-1.aws.neon.tech/neondb?sslmode=require`.

(Supabase also works: Project Settings → Database → Connection string → "Transaction pooler" URI.)

### 2. Code on GitHub

1. Create a new **private** repository on https://github.com/new (for example `our-rentals`).
2. Upload all the files in this folder (not `node_modules` or `.next`). On the repository page: **Add file → Upload files**, drag the folder contents in, then **Commit**.

### 3. Website (Vercel, free)

1. Go to https://vercel.com, sign up with GitHub.
2. **Add New → Project**, pick the `our-rentals` repository, click **Import**.
3. Open **Environment Variables** and add:

   | Name | Value |
   |---|---|
   | `DATABASE_URL` | the Neon connection string |
   | `APP_PASSWORD` | the everyday password for your dad |
   | `ADMIN_PASSWORD` | your admin password (different!) |
   | `SESSION_SECRET` | any long random text, e.g. 40 random letters |
   | `CONTACT_PHONE` | (optional) phone shown on the /available page |

4. Click **Deploy**. After a minute you get a link like `https://our-rentals.vercel.app`.
5. Open it on your dad's phone and use **Add to Home Screen** so it opens like an app.

Changing a password later: Vercel → Project → Settings → Environment Variables → edit → then Deployments → Redeploy.

---

## Running it on a computer (for developers)

```bash
npm install
cp .env.example .env.local   # fill in the values
npm run dev                  # open http://localhost:3000
```

Tables are created automatically on first use. Built with Next.js and PostgreSQL.
