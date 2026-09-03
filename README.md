# Personal Archive

Single-file vanilla HTML/CSS/JavaScript personal digital archive using Firebase Authentication, Cloud Firestore and GitHub repository storage, hosted on GitHub Pages.

## Firebase setup
1. Enable Authentication -> Email/Password.
2. Create a Firestore database.
3. Deploy `firestore.rules` in the Firebase console or with the Firebase CLI.
4. Firebase Storage is not required.

## GitHub archive storage
The website stores archive file metadata in Firestore and the actual uploaded file bytes in a GitHub repository through the GitHub REST API.

In Admin -> Archive files, enter:
- Repository owner
- Repository name
- Branch (normally `main`)
- A fine-grained GitHub personal access token with **Contents: Read and write** permission for that repository

The token is held only in the current browser tab's memory and is never saved to Firestore or committed to the repository. A page reload requires entering it again.

The GitHub Contents API is used to create/update repository files with Base64 content and to delete them again.

### Public/private limitation
For a static GitHub Pages site, files intended for anonymous public visitors need to be reachable without authentication. Therefore public archive records use a `raw.githubusercontent.com` URL. If the repository itself is private, those raw URLs cannot be used as anonymous public downloads. The Firestore `public` field controls whether the record is shown by the site; it does not turn a public GitHub repository into private storage.

## GitHub Pages
Push the repository to GitHub and enable Settings -> Pages -> Source -> GitHub Actions. The included workflow deploys the static site.

## Sharing QR
The Website QR section generates a branded QR for the public homepage. The administrator can enable the same QR on the Contact page.

## Security note
Do not hard-code a GitHub token in `index.html`. The interface intentionally asks the administrator for the token at runtime and keeps it only in memory. A browser-side token is still exposed to the page while the admin session is active, so use a fine-grained token restricted to only the repository that stores this archive.
