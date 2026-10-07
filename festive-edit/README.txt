THE FESTIVE EDIT — gift choice form
===================================

Upload to GitHub Pages (root of the repo):

    index.html
    results.html
    assets/gift-1.png
    assets/gift-2.png
    assets/gift-3.png
    assets/gift-4.jpeg

Keep the "assets" folder name exactly as-is — the page loads
the images as assets/gift-1.png etc.

DO NOT upload the "_apps-script (do not upload)" folder.
That file goes into the Apps Script editor instead.

----------------------------------------------------------------
Both HTML files are already wired to your live script URL.
Nothing to edit in them.
----------------------------------------------------------------

STILL TO DO IN APPS SCRIPT (Code-GiftChoice.gs):
  line 19  POWER_AUTOMATE_URL  — your email webhook
  line 24  VIEW_PASSWORD       — change from 'change-me-now'
Then: Deploy > Manage deployments > edit > New version > Deploy.

URLS ONCE PAGES IS ON:
  Employees :  https://YOURNAME.github.io/YOURREPO/
  HR        :  https://YOURNAME.github.io/YOURREPO/results.html

HEALTH CHECK:
  Open your /exec URL with nothing after it. You should see
  {"success":true,"pong":true,"version":"1.0-gift", ...}

BEFORE SENDING THE LINK OUT:
  1. Do one test submission with your own email.
  2. Check the Choices tab, the confirmation email, and that
     reopening the link shows your gift locked.
  3. Delete your test row from the sheet.
