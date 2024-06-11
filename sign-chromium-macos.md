

# 1. Install Apple's Certificate Authority certificates

To sign a Chromium app on macOS, you need to download the "Developer ID - G2" and "Worldwide Developer Relations - G3" certificates from [Apple's Certificate Authority](https://www.apple.com/certificateauthority/).
![Apple's Certificate Authority](./img_mac_sign/download-apple-intermediate-certificates.png)

You can install the two downloaded files by double-clicking on them.
![Install certificates](./img_mac_sign/apple-intermediate-certificates.png)

Open Keychain Access.

<img src="./img_mac_sign/open-keychain-access.png" width="500" />

You can see 2 certificates in Keychain Access.

![Keychain Access](./img_mac_sign/keychain-access.png)

# 2. Create and install "Mac Development" certificate.

Request a Certificate From a Certificate Authority.

![Request a Certificate 01](./img_mac_sign/request-certificate-01.png)
![Request a Certificate 02](./img_mac_sign/request-certificate-02.png)
![Request a Certificate 03](./img_mac_sign/request-certificate-03.png)

Generated CertificateSigningRequest.certSigningRequest in Desktop.

![Request a Certificate 04](./img_mac_sign/request-certificate-04.png)


Open the Certificates section on the Apple Developer account.

![developer-certificate-01](./img_mac_sign/developer-certificate-01.png)

![developer-certificate-02](./img_mac_sign/developer-certificate-02.png)

![developer-certificate-03](./img_mac_sign/developer-certificate-03.png)

![developer-certificate-04](./img_mac_sign/developer-certificate-04.png)

![developer-certificate-05](./img_mac_sign/developer-certificate-05.png)

![developer-certificate-06](./img_mac_sign/developer-certificate-06.png)

![developer-certificate-07](./img_mac_sign/developer-certificate-07.png)

You can install the downloaded certificate file by double-clicking on it.

Mac Development certificate is successfully installed, as shown in the screenshot below.

![developer-certificate-08](./img_mac_sign/developer-certificate-08.png)


# 3. Sign the MultiOn.app with the Mac Development certificate.

Run the following command in chromium/src folder.

```
$ ninja -C out/release chrome chrome/installer/mac
```

After running the command, you will notice a newly created "MultiOn Packaging" folder in the "out/release" directory.

./out/release/MultiOn\ Packaging/sign_chrome.py --input out/release --output out/release/signed --identity 'Your Mac Developer ID' --development --disable-packaging

You should replace the copied ID from Keychain Access instead of "Your Mac Developer ID."

![Your Mac Developer ID](./img_mac_sign/Your%20Mac%20Developer%20ID.png)



After above command, you can find the MultiOn.app in the "out/release/signed/stable" folder. 

To check if the sign is correct, you can run the following command:

```
codesign --verify --deep --strict --verbose=2 path/to/MultiOn.app
```

Or

```
codesign -dvvv path/to/MultiOn.app
```

You can run the MultiOn.app on another PC once it has been signed with the Mac Development certificate.

To run it on another PC, simply click "Open" in the right-click menu of the MultiOn.app.

![run on another pc](./img_mac_sign/run-multion-another-pc.png)
