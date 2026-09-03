# Personal Archive

A single-file personal digital archive using:

- GitHub Pages for hosting
- Firebase Authentication for the administrator login
- Cloud Firestore for articles, events, pages, navigation, settings, and archive metadata
- GitHub repository files for public archive files
- No Firebase Cloud Storage
- No localStorage/database in the browser

## Firebase configuration

The provided Firebase web configuration is already included in `index.html`.
If you change Firebase projects, replace the `firebaseConfig` object in the HTML with the new web app configuration.

## Archive files

Put public archive files in `archive/`, commit/push them to GitHub, then register their metadata in Admin -> Archive files.
The website accepts either a repository-relative path such as `archive/example.pdf` or a direct URL.

A public GitHub repository cannot provide truly private file storage. The archive record can be private in Firestore, but a file physically present in a public repository remains publicly accessible if someone knows its URL. For genuinely private files, use a provider that enforces access permissions (for example a restricted Google Drive file) and store its URL as the archive record's direct URL.

## Firebase rules

`firestore.rules` is included. It allows public users to read only public records, while authenticated administrators can manage all content.

The first administrator is created through the website's first-run Admin screen. After setup is initialized, the rules prevent additional admin records from being created through the client.

## GitHub Pages

The included `.github/workflows/pages.yml` deploys the repository to GitHub Pages whenever `main` is updated.

In GitHub:
1. Repository -> Settings -> Pages.
2. Under Build and deployment, choose GitHub Actions.
3. Push the repository.
4. Wait for the Pages workflow to finish.

## Local test

From the repository directory:

    python3 -m http.server 8080

Then open:

    http://localhost:8080/

Do not use a `file://` URL for the final Firebase test.

## Admin

The admin dashboard is not shown in public navigation. Open the site and add `#admin` to the URL, for example:

    https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/#admin

On the first run, create the administrator. Later visits show the login form.

## Important security notes

- Never put a GitHub personal access token in `index.html`.
- Never put Firebase Admin SDK/service-account credentials in the website.
- Keep Firestore rules deployed and do not use `allow read, write: if true` in production.
- The Firebase web API key is not a secret; authorization is provided by Firebase Auth and Firestore Security Rules.
