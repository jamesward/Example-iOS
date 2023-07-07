# Example-iOS
An example of how to use Apple development GitHub Actions

1. Get App Store Team ID from: https://developer.apple.com/account#MembershipDetailsCard
2. Store App Store Team ID in GitHub Secret: `APPSTORE_TEAM_ID`
1. Create Identifier for *App IDs* https://developer.apple.com/account/resources/identifiers/list
1. Store in GitHub Secret: `BUNDLE_ID`
1. Create *App Store Connect API* https://appstoreconnect.apple.com/access/api
1. Store Issuer ID in GitHub Secret: `APPSTORE_ISSUER_ID`
1. Generate API Key with Access `App Manager`
1. Store Key ID in GitHub Secret: `APPSTORE_KEY_ID`
1. Store Private Key in GitHub Secret: `APPSTORE_PRIVATE_KEY`

1. Generate a Private Key for signing:
    `openssl genrsa -out mykey.key 2048`
1. Generate a Certificate Signing Request:
    ```
    export EMAIL=YOUR_EMAIL
    export NAME="YOUR_NAME"
    openssl req -new -key mykey.key -out CertificateSigningRequest.certSigningRequest -subj "/emailAddress=$EMAIL, CN=$NAME, C=US"
    ```
1. Add a new Certificate of *Apple Development* https://developer.apple.com/account/resources/certificates/add
1. Upload the `CertificateSigningRequest.certSigningRequest`
1. Download the certificate
1. Convert the cert to PEM format:
    `openssl x509 -in development.cer -inform DER -out development.pem -outform PEM`
1. Add a new Certificate of *Apple Distribution* https://developer.apple.com/account/resources/certificates/add
1. Upload the `CertificateSigningRequest.certSigningRequest`
1. Download the certificate
1. Convert the cert to PEM format:
   `openssl x509 -in distribution.cer -inform DER -out distribution.pem -outform PEM`
1. Combine the two certs:
    `cat development.pem distribution.pem > cert.pem`
1. Export the p12 remembering the password:
   `openssl pkcs12 -export -legacy -inkey mykey.key -in cert.pem -out cert.p12`
1. Store the password in GitHub Secret: `CERTIFICATES_PASSWORD`
1. Convert the cert to Base64 and store in GitHub Secret: `CERTIFICATES_P12`
    `base64 cert.p12`
1. Create `iOS App Development` Provisioning Profile: https://developer.apple.com/account/resources/profiles/add
1. Store the name of the provisioning profile in GitHub Secret: `DEV_PROVISIONING_PROFILE_NAME`
1. Create `App Store` Provisioning Profile: https://developer.apple.com/account/resources/profiles/add
1. Store the name of the provisioning profile in GitHub Secret: `DIST_PROVISIONING_PROFILE_NAME`
