# Publishing a Release

This project uses a manually-invoked GitHub Actions workflow to publish its packages.

This workflow uses:
- The SLSA Node.js builder to achieve SLSA v3-level provenance
- An NPM granular access token for `achrinza-bot`

## Publishing

Before continuing, enusre that you have:

1. A GitHub account with the `Repository Admin` role for the `achrinza/node-ipc` repository
2. The username and password for the `achrinza-bot` NPM account or any account that has:
  1. TOTP 2FA enabled
  2. Write access to the `@achrinza/node-ipc` NPM package
3. The TOTP generator for said account

### 1. Regenerating the NPM Granular Token
1. Go to [New Granular Access Token](https://www.npmjs.com/settings/achrinza/tokens/granular-access-tokens/new)
2. Generate a granular access token that:
  1. expires in 1 day
  2. has `Read and write` permssions for only the `@achrinza/node-ipc` package.
3. Click `Generate` and copy the token
4. Go to [Update Action secret NPM_TOKEN](https://github.com/achrinza/node-ipc/settings/secrets/actions/NPM_TOKEN)
5. Paste the token and click `Update secret`

### 2. Creating a GitHub "Release"

1. Delete and re-fetch all Git tags
   This is necessary to prevent accidental tags from being pushed to the GitHub repository
   
   On Linux or macOS:
   ```sh
   $ git branch -l | xargs -I{} git branch -d {}
   $ git fetch 'refs/tags/*:refs/tags/*'
   ```

2. De

### 3. Creating an NPM Release

> [!NOTE]
> Ensure the Git comit and tag from the previous step has been completed

3. Go to [CD * workflow runs](https://github.com/achrinza/node-ipc/actions/workflows/cd.yaml)
