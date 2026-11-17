Holcim UK New Manager Toolkit
Served at new-manager-toolkit.vercel.app

WHAT THIS IS
Static HTML pages. No server-side code, no database, no sign-in logic. Host the folder as-is; index.html is the Manager tools page.

FILES
  index.html                            Manager tools (the home page)
  Manager Career Conversation Kit.html  Career Conversation Kit for line managers
  Development Plan.html                 Development Plan (IDP builder)
  Your Career Tools.html                Colleague hub
  vendor/                               Libraries bundled locally:
                                          react.production.min.js      React 18.3.1
                                          react-dom.production.min.js  React DOM 18.3.1
                                          babel.min.js                 Babel standalone 7.29.0. Used by build.js only; pages do not load it
  src/                                  Editable source (JSX) for the two React pages
  build.js                              Compiles src/ into the pages

These pages are kept in step with the same pages in holcim-uk/colleague-career-tool. When one changes there, copy it here too (and src/ if it is a React page).

CHANGING A PAGE
The Development Plan and the Manager Career Conversation Kit are React pages. Their code is written in JSX and compiled to plain JavaScript in advance, so browsers do not have to run Babel on every visit.

  1. Edit its file in src/ (development-plan.jsx or manager-career-conversation-kit.jsx). HTML and CSS outside the script stay in the .html file.
  2. Run:  node build.js      (needs Node.js; nothing to install)
  3. Commit both the src/ file and the updated .html file.
  Do not edit the compiled block in the .html file: the next build overwrites it.

  If you upload a fresh export that still contains <script type="text/babel">, run "node build.js": it saves the new code into src/ and compiles the page.
  "node build.js --check" lists any page that has not been built, without changing anything.

KNOWN GAPS
  - Your Career Tools links to "Holcim Career Reflections.html", which is not in this repository.

HOSTING REQUIREMENTS
  - Serve over HTTPS. The Development Plan and the Career Conversation Kit save entries in browser localStorage only; nothing is sent anywhere. Keep the pages on one domain and path so saved entries are found again.
  - The pages load Montserrat and Reddit Sans from Google Fonts (fonts.googleapis.com, fonts.gstatic.com). If that is blocked they fall back to the system font.
  - Content Security Policy: inline <script> and <style> blocks are used, so allow 'unsafe-inline'. 'unsafe-eval' is not needed.
