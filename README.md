# ssl-android-fix
Fix issue of SSL Handshake Exception on Android : Trust anchor for certification path not found

The change on the app to use a secured URL broke the entire app.
Below is what the the error on the log was like :
```
<-- HTTP FAILED: javax.net.ssl.SSLHandshakeException: java.security.cert.CertPathValidatorException: Trust anchor for certification path not found.
```
## Step 1
Add the cer file to the raw folder.
projet-name/src/main/res/raw/myawesomeca.cer

## Step 2
Create network_security_config.xml
projet-name/src/main/res/xml/network_security_config.xml
And paste :
```bash
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <domain-config>
        <domain includeSubdomains="true">57.129.53.74</domain>
        <trust-anchors>
            <certificates src="@raw/myawesomeca"/>
        </trust-anchors>
    </domain-config>
</network-security-config>
```

## Step 3
Configure manifest
mifosng-android/src/main/AndroidManifest.xml
Add in <application 
          ...
          application/>:
```bash
android:networkSecurityConfig="@xml/network_security_config"
```

## That is all
