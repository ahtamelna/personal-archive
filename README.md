# Personal Archive

Static GitHub Pages personal archive with Firebase Authentication/Firestore for admin/content data and GitHub repository storage for archive files.

## GitHub archive storage

The admin dashboard uses GitHub's REST API Contents endpoint to upload, replace, and delete archive files. GitHub documents that this endpoint supports fine-grained personal access tokens with repository **Contents: write** permission.

The token is intentionally NOT stored in Firestore, the repository, or the HTML source. It is entered by the administrator in Admin > Archive files and kept only in JavaScript memory for the current browser tab. Reloading the page clears it.

For a public GitHub repository, public archive files can be served through `raw.githubusercontent.com`. A private repository is not a public file host; private files require authenticated access and therefore cannot be exposed as ordinary public download links from a static GitHub Pages site.

## Setup

1. Enable Firebase Authentication > Email/Password.
2. Enable Firestore and publish `firestore.rules`.
3. Put this project in a GitHub repository and enable GitHub Pages with GitHub Actions.
4. Open the site and go to Admin.
5. Initialize the administrator.
6. Open Admin > Archive files.
7. Enter the GitHub repository owner, repository name, branch, and a fine-grained token with Contents: write permission for that repository.
8. Click Use this repository, then Add file.

Never commit the token to the repository and never put it into the HTML source.
