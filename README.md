# MTA-STS Policy for startree.ai

This repository hosts the **Mail Transfer Agent - Strict Transport Security (MTA-STS)** policy file for the `startree.ai` domain. 

It is served publicly via GitHub Pages to enforce encrypted email transit (TLS) for all incoming messages, protecting against Man-in-the-Middle (MitM) and downgrade attacks.

## 🏗️ Architecture
* **Live URL:** `https://mta-sts.startree.ai/.well-known/mta-sts.txt`
* **Hosting:** GitHub Pages.
* **Important Note:** The `.nojekyll` file in the root directory is strictly required. Without it, GitHub Pages will ignore the `.well-known` folder and return a 404 error.

## 📝 How to Update the Policy
If we need to update our allowed MX servers or switch the policy from `testing` to `enforce`, follow these exact steps:

1. **Update the Text File:** Edit `mta-sts.txt` inside the `.well-known` directory and commit to `main`.
2. **Wait for Deployment:** Allow GitHub Pages a minute or two to rebuild.
3. **UPDATE THE DNS RECORD (CRITICAL):** External mail servers cache this file. To force them to fetch the new version, you **must** update the `_mta-sts` TXT record in our DNS provider. 
   * Change the `id=` value to the current timestamp.
   * *Example:* Change `v=STSv1;id=<OLD_TIMESTAMP>;` to `v=STSv1;id=<NEW_CURRENT_TIMESTAMP>;`
