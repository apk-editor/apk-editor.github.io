---
layout: default
title: Signing APK's
permalink: /apk-signing/
---

<style>
    tab1 { padding-left: 4em; }
</style>

## APK Signing

<p style="text-align: justify;"><tab1>AEE will recognize APK files and app bundles and sign them accordingly with its default key. In order to sign an APK using a custom Keystore, some specific methods need to be followed and are explained in the next section.</tab1></p>

## Signing with a custom key

<p style="text-align: justify;"><tab1>In order to sign APK's with a custom key, AEE requires either a <b>PKCS #12</b> keystore or a <b>PKCS #8</b>/<b>X509Certificate</b> key pair.</tab1></p>

### How to generate a PKCS #12 keystore

<ol>
    <li>Convert a java keystore (JKS) to PKCS12 format<br><br><b>keytool -importkeystore -srckeystore KEYSTORE_PATH -destkeystore intermediate.p12 -srcstoretype JKS -deststoretype PKCS12</b><br><br></li>
</ol>

### How to create a PKCS #8 private key

<ol>
    <li>Convert a PKCS12 to pem format<br><br><b>openssl pkcs12 -in intermediate.p12 -nodes -out intermediate.rsa.pem</b><br><br></li>
    <li>Convert the pem file to PKCS #8 format<br><br><b>openssl pkcs8 -topk8 -outform DER -in intermediate.rsa.pem -inform PEM -out private.pk8 -nocrypt</b><br></li>
</ol>

### How to create X509Certificate

<ol>
    <li>Read X509Certificate from a java keystore (JKS)<br><br><b>keytool -list -rfc -keystore KEYSTORE_PATH -alias KEY_ALIAS -storepass STORE_PASSWORD</b><br><br></li>
    <li>From the output, copy the text starting from <b>-----BEGIN CERTIFICATE-----</b> to <b>-----END CERTIFICATE-----</b> (including both) and save it as a text file<br><br></li>
</ol>

### Configure AEE to work with custom key

<p style="text-align: justify;"><tab1>Open AEE and Navigate to <b>Settings -> Sign APK's with</b> and select <b>Custom Key</b>. A new page will now open which offers an option to select a custom <b>Private Key</b>. Use it to import your PKCS #12 keystore or PKCS #8 private key. Depending on the imported file, AEE might ask for additional details. For e.g., keystore and alias passwords are requested upon importing a PKCS #12 keystore. On the other hand, importing a PKCS #8 private key to AEE will lead you to a new window requesting it's respective X509Certificate pair. By fulfilling them, AEE will do the following changes, and now onwards uses the new credentials for signing.</tab1></p>

<ol>
    <li>Save private key as<br><br><b>/data/data/com.apk.editor/files/signing/APKEditor.pk8</b><br><br></li>
    <li>Save X509Certificate as<br><br><b>/data/data/com.apk.editor/files/signing/APKEditorCert</b><br><br></li>
</ol>

<p style="color: blue; text-align: start"><a href="{{ site.github.url }}/general/">Previous: <b>General</b></a></p>
