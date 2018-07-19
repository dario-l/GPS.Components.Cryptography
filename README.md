# GPS.Components.Cryptography

.NET Library for signature Xades-BES and PKCS#7. The library is used for signature by XADES-BES and PKCS # 7 method

## Methods

The EDeklaracja object in the namespace of GPS.Components.Cryptography.EDeklaracje provides static **main methods**:

```
public static XmlDocument PodpiszXades(XmlDocument doc, X509Certificate2 cert, CryptType cryptType)

public static XmlDocument PodpiszXades(string content, X509Certificate2 cert, CryptType cryptType)

public static byte[] PodpiszXadesByte(XmlDocument doc, X509Certificate2 cert, CryptType cryptType, ref XmlDocument signedXml)

public static byte[] PodpiszXadesByteZbiorczy(string base64String, X509Certificate2 cert, CryptType cryptType, ref XmlDocument signedXml)

Parameter @CryptType - SHA1, SHA256 (enum)
```
and helpers:

```
public static X509Certificate2 SelectCertificate (string title, string description)        
    
public static X509Certificate2 GetCertificate(object findValue, X509FindType findType)
    
public static byte[] PodpiszPKCS7(byt [] content, CmsSigner signer)

public static void PodpiszPKCS7(string fileName, string signedFileName, CmsSigner signer)

public static byte[] GetByte(object obj)

public static byte[] GetByte64(object obj)

public static byte[] GetByte64(object obj, ref string xml)

public static byte[] GetByte64(byte [] byteArray)
```

## Examples

```
XmlDocument signed = new XmlDocument();
    
byte[] byte = EDeklaracja.PodpiszXadesByte(doc, this.X509Certificate, ref signed);
```
## Example Signature

The signature is compatible for the "e-deklaracje" system in Poland

```
<Signature Id="Signature-3f81fc13-92cf-4dcb-9e79-cc952e15cf20" xmlns="http://www.w3.org/2000/09/xmldsig#">
    <SignedInfo>
      <CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
      <SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" />
      <Reference Id="Signature-3f81fc13-92cf-4dcb-9e79-cc952e15cf20-XADES-Properties-Ref" URI="#XADES-Properties" Type="http://uri.etsi.org/01903/v1.1.1#SignedProperties">
        <Transforms>
          <Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
        </Transforms>
        <DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />
        <DigestValue>G7+YKloCz86fHOCTuxwi1CpCdGHE6+b2iB9N5ef4T48=</DigestValue>
      </Reference>
      <Reference Id="Signature-3f81fc13-92cf-4dcb-9e79-cc952e15cf20-KeyInfo-Ref" URI="#KeyInfo">
        <Transforms>
          <Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
        </Transforms>
        <DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />
        <DigestValue>Axmid1gAEDyUBHAF7gVmlCkHg4XPN7zSnxT5aLko6lc=</DigestValue>
      </Reference>
    </SignedInfo>
    <SignatureValue>wUobDCNSKg31kJARp4GB9VuK3tYlVZh00uXJ4u4XiEHPd6gnurI0gytKjnuzUxqV4dBHac5Fg5DsCEdfA+yIhgl9Rm5h9cokpKE5cxpAJMeSb1dDj/ilEgDF7Dl1096HkXIlmfG57Ud4a/3vTIfC1CWM5YmLvD8CdFq8AIn6a9lJvZSURFyu87s2hU5HEFovVP2MeNpWxczMVXxUslpl0UjMtl9zIzm5e1nP/GnX4Trdzdz+JAImLIRPTWcpxqIHEWPkw9AfIg5+BR62Oq21wWEf8KtnC0RiiYwB4/CfpzWJjtG3WKl3cexLPd/YHxDa6LwqL974jTRGzaib7itl8A==</SignatureValue>
    <KeyInfo Id="KeyInfo">
      <X509Data>
        <X509SubjectName>CN=*.piotrkobylski.com, O=DO_NOT_TRUST, OU=Created by http://www.piotrkobylski.com</X509SubjectName>
        <X509Certificate>MIIDTDCCArWgAwIBAgIQNWCmCaFc9ZJC3lIAcfGadDANBgkqhkiG9w0BAQsFADBnMSswKQYDVQQLDCJDcmVhdGVkIGJ5IGh0dHA6Ly93d3cuZmlkZGxlcjIuY29tMRUwEwYDVQQKDAxET19OT1RfVFJVU1QxITAfBgNVBAMMGERPX05PVF9UUlVTVF9GaWRkbGVyUm9vdDAeFw0xNTA5MjMxNTM4NDFaFw0yMTA5MjIxNTM4NDFaMFsxKzApBgNVBAsMIkNyZWF0ZWQgYnkgaHR0cDovL3d3dy5maWRkbGVyMi5jb20xFTATBgNVBAoMDERPX05PVF9UUlVTVDEVMBMGA1UEAwwMKi5naXRodWIuY29tMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAx9LDIsXb4f/gdo5bSzMUv5O3+wJdAsXzuz/DzfpGHTtYP8Nqc/Nzwte+1MAbmfkeGksx5PtnKW8KOtsSTsdWNk0v9v6cn7Q6o1Q/lMJawfLIV7t+tFYMuxehgfsYB85PxQ1XGh2OAXW7xvXdXsb3ZM352iHnwHNF8KyQuoF85FkfxWPDRQgteJmZvyE5hZEVA7Iwmw4nYZH8cixUaBSNSDmwaJyUipwCkm6ZMKttjWsYX10mEL05p+ggiLQjQxws2i9LBIzfsR1a7qj3/3k36fphtuu5PIpSwool7pvRzG3HuvQfq1048ztmQplFCy7EabvFvdUCDX2BaJXTq2h2UQIDAQABo4GAMH4wDgYDVR0PAQH/BAQDAgSwMBMGA1UdJQQMMAoGCCsGAQUFBwMBMBcGA1UdEQQQMA6CDCouZ2l0aHViLmNvbTAfBgNVHSMEGDAWgBRJMEiCq1b2KSEo0lRxgcTaeAigjTAdBgNVHQ4EFgQUFe171sNb9JN4LEzmHmO+WAP22jswDQYJKoZIhvcNAQELBQADgYEAbRwAguYYkycqcmhMHUKjp2si39iGo+3qugi6m0lFS85YWJDOma/S2K62PzBSIdLLuCq6v8oi4/6eiI7DBMj+jjRFgMCOTXzNl6JSP5bqHMIX+U1sjLqEczaA8KqGDkTGyP6I7JBYnHdYBCKLWPkltIFUHOlEyycFeCaX6kGojuc=</X509Certificate>
      </X509Data>
    </KeyInfo>
    <Object Id="XADES">
      <xades:QualifyingProperties Target="Signature-3f81fc13-92cf-4dcb-9e79-cc952e15cf20" xmlns:xades="http://uri.etsi.org/01903/v1.3.2#">
        <xades:SignedProperties Id="XADES-Properties">
          <xades:SignedSignatureProperties>
            <xades:SigningTime>2018-07-19T21:26:48Z</xades:SigningTime>
            <xades:SigningCertificate>
              <xades:Cert>
                <xades:CertDigest>
                  <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" xmlns:ds="http://www.w3.org/2000/09/xmldsig#" />
                  <ds:DigestValue xmlns:ds="http://www.w3.org/2000/09/xmldsig#">OZxcvpyaH+nykGgYZaipqx8AXvoi8TEZs+18qEppvbU=</ds:DigestValue>
                </xades:CertDigest>
                <xades:IssuerSerial>
                  <ds:X509IssuerName xmlns:ds="http://www.w3.org/2000/09/xmldsig#">CN=DO_NOT_TRUST_Root, O=DO_NOT_TRUST, OU=Created by http://www.piotrkobylski.com</ds:X509IssuerName>
                  <ds:X509SerialNumber xmlns:ds="http://www.w3.org/2000/09/xmldsig#">3560A609A15CF59242DE520071F19A74</ds:X509SerialNumber>
                </xades:IssuerSerial>
              </xades:Cert>
            </xades:SigningCertificate>
          </xades:SignedSignatureProperties>
        </xades:SignedProperties>
      </xades:QualifyingProperties>
    </Object>
  </Signature>
```

## Licence

Library only for testing purposes
