THE FESTIVE EDIT — gift choice form
===================================

UPLOAD TO GITHUB (at the ROOT of the repo, not in a subfolder):
    index.html
    results.html
    assets/gift-1.png  gift-2.png  gift-3.png  gift-4.jpeg

Keep the folder named exactly "assets".
DO NOT upload "_apps-script (do not upload)".

Both HTML files are already wired to your script URL. Nothing to edit.

=================================================================
SETUP ORDER  (personal links — do these in order)
=================================================================

0. YOUR OWN EMAIL WORDING (optional)
   Paste your prepared text into INVITE_BODY near the top of
   Code-GiftChoice.gs. Plain text, blank line between paragraphs,
   no HTML needed. Use {{first}} for the first name and {{name}}
   for the full name. The navy header and each person's personal
   "Choose my gift" button are added automatically.
   Also settable: INVITE_SUBJECT, INVITE_HEADING,
                  REMINDER_SUBJECT, REMINDER_BODY,
                  INVITE_SIGNOFF   (e.g. "Warm regards,")
                  INVITE_SIGNATURE (the HR person's name)
   The sign-off appears on the invitation AND the confirmation email.
   If you sign off inside INVITE_BODY, set INVITE_SIGNOFF to ''
   so you do not get two sign-offs.
   Leave INVITE_BODY as '' to use the default wording.

1. Paste Code-GiftChoice.gs into Apps Script. Set:
      line 19  POWER_AUTOMATE_URL  — your email webhook
      line 23  VIEW_PASSWORD       — change from 'change-me-now'
      line 32  FORM_URL            — your GitHub Pages URL
                                     (e.g. https://you.github.io/gifts/)
   Deploy > Manage deployments > pencil > New version > Deploy.

2. Upload the HTML + assets to GitHub, turn on Pages, and confirm the
   page loads. Put that URL into FORM_URL above if you hadn't yet,
   then redeploy.

3. In the Sheet, open the "Roster" tab (run buildRosterLinks once and
   it is created for you). Fill in, from row 2 down:
      A Name      B Email      C Phone (optional)

4. Run buildRosterLinks() from the Apps Script editor.
   It fills column D (token) and column E (Personal Link).
   Safe to re-run later when you add more people — existing
   links are never changed.

5. Run testInvitation() to see the email in your own inbox first
   (edit the address inside the function).

6. Run sendInvitations(). It emails each person their own link,
   one message each — no mail merge needed. It stamps column H
   so nobody is ever mailed twice; re-run it after adding more
   people and only the new ones get mailed.

   NEVER send one link to everybody — a link identifies the person.

=================================================================
HOW THE LOCK WORKS
=================================================================
Opening a personal link pre-fills name / email / phone from the
Roster and locks those fields. The server takes identity from the
token, never from what the page sends, so editing the page in a
browser achieves nothing.

Without a valid link, nothing can be submitted at all.

Only @luckmans.com and @accubooks.in addresses can be given links
(buildRosterLinks skips anything else and tells you which rows).

To switch back to an open form: set REQUIRE_TOKEN = false (line 41).

=================================================================
USEFUL FUNCTIONS (Apps Script editor, Run menu)
=================================================================
  buildRosterLinks()      generate personal links
  testInvitation()        preview the invite email (edit address first)
  sendInvitations()       email everyone their own link (skips those done)
  sendReminders()         nudge only those who haven't chosen yet
  refreshRosterStatus()   fill Chosen / Gift columns on the Roster
  remindersOutstanding()  list who still hasn't chosen (+ their links)
  showTally()             running count per gift, for ordering
  testEmail()             smoke-test the confirmation email

HEALTH CHECK — open your /exec URL with nothing after it:
  {"success":true,"pong":true,"version":"1.5-gift-signature",
   "requireToken":true, ...}

URLS
  Employees :  their personal link (column E)
  HR        :  https://YOURNAME.github.io/YOURREPO/results.html

BEFORE SENDING TO EVERYONE
  1. Add yourself to the Roster, run buildRosterLinks, open your own
     link and submit a test choice.
  2. Check: fields pre-filled and locked, row in Choices tab,
     confirmation email received, reopening shows the gift locked.
  3. Delete your test row from Choices, then run refreshRosterStatus.
