Holcim UK New Manager Toolkit
Served at new-manager-toolkit.vercel.app

WHAT THIS IS
Static HTML pages. No server-side code, no database, no sign-in logic. Host the folder as-is; index.html is the Manager tools page.

FILES
  index.html                            Manager tools (the home page)
  Manager Career Conversation Kit.html  Career Conversation Kit for line managers
  vendor/                               Libraries bundled locally:
                                          react.production.min.js      React 18.3.1
                                          react-dom.production.min.js  React DOM 18.3.1
                                          babel.min.js                 Babel standalone 7.29.0. Used by build.js only; pages do not load it
  src/                                  Editable source (JSX) for the Career Conversation Kit
  build.js                              Compiles src/ into the pages

COLLEAGUE PAGES LIVE ON THE COLLEAGUE SITE
Colleague-facing pages (Your Career Tools, Career Reflections, the Development Plan, Career Conversation Prep) are not copied here. They live in holcim-uk/colleague-career-tool, served at https://colleague-career-tool.vercel.app/, and this site links to them. Keeping one copy means fixes only need making once, and each person's saved notes stay in one place: browsers keep saved entries separately for each website.
  - Manager tools "Discover" for the Development Plan opens https://colleague-career-tool.vercel.app/Development%20Plan.html in a new tab.
  - "Your career tools" goes to https://colleague-career-tool.vercel.app/Your%20Career%20Tools.html
  If the colleague site moves (for example to Blink), update those links in index.html.

The Career Conversation Kit also exists in holcim-uk/colleague-career-tool. When it changes there, copy the .html file and src/manager-career-conversation-kit.jsx here too.

CHANGING A PAGE
The Manager Career Conversation Kit is a React page. Its code is written in JSX and compiled to plain JavaScript in advance, so browsers do not have to run Babel on every visit.

  1. Edit src/manager-career-conversation-kit.jsx. HTML and CSS outside the script stay in the .html file.
  2. Run:  node build.js      (needs Node.js; nothing to install)
  3. Commit both the src/ file and the updated .html file.
  Do not edit the compiled block in the .html file: the next build overwrites it.

  If you upload a fresh export that still contains <script type="text/babel">, run "node build.js": it saves the new code into src/ and compiles the page.
  "node build.js --check" lists any page that has not been built, without changing anything.

HOSTING REQUIREMENTS
  - Serve over HTTPS. The Career Conversation Kit saves entries in browser localStorage only; nothing is sent anywhere. Keep the pages on one domain and path so saved entries are found again.
  - The pages load Montserrat and Reddit Sans from Google Fonts (fonts.googleapis.com, fonts.gstatic.com). If that is blocked they fall back to the system font.
  - Content Security Policy: inline <script> and <style> blocks are used, so allow 'unsafe-inline'. 'unsafe-eval' is not needed.
