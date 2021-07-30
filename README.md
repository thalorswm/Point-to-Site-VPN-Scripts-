# Point-to-Site-VPN-Scripts

Before Generating certificates we need to go mmc (microsoft management console) -> File (option) -> Go to add/remove snap (option) -> add certificates -> Personal Folder (where we will see all certificates )

------------------------------
For Generating Certificates 
------------------------------
-> Go to Powershell ISE (Run as Admin)
#self signed root certificate

$cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign

This Script will create root certificate 

#client side cerfiticate

New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")

This Script will create client certificate
