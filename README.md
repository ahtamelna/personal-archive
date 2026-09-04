# Personal Archive

Single-file vanilla HTML/CSS/JavaScript personal digital archive using Firebase Authentication, Cloud Firestore and GitHub repository storage, hosted on GitHub Pages.

## Firebase setup
1. Enable Authentication -> Email/Password.
2. Create a Firestore database.
3. Deploy `firestore.rules` in the Firebase console or with the Firebase CLI.
4. Firebase Storage is not required.

## GitHub archive storage
In Admin -> Archive files, enter the GitHub account username, repository name, branch and token. The connection is stored in the admin-only Firestore document `github/config` so it is available after signing in again.

Use a fine-grained GitHub token with Contents: Read and write permission for the archive repository.

Uploaded archive files are committed under the repository's `archive/` directory. Firestore stores the archive records and their settings. Public files are served through the GitHub Pages site, so the repository must be public if those files need to be accessible to visitors without GitHub authentication.

## GitHub Pages
Push the repository to GitHub and enable Settings -> Pages -> Source -> GitHub Actions. The included workflow deploys the static site.

## Content
The admin dashboard includes articles, a standalone Featured page, archive files, featured archive files, calendar actions, custom pages, navigation links, site content and account management.

Articles are written directly in the dashboard rather than in a popup. The home page can display today's public action and selected featured archive files.

## Security
The GitHub connection is stored in an admin-only Firestore document and is not included in the public site content. Use a fine-grained token limited to the archive repository and keep the Firestore rules deployed.
