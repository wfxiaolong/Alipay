## Signature Algorithms

### Generate Pre-sign string

**Parameters to sign**

In the list of request and response parameters, all of them need to be signed except sign and sign_type. (sign_type also needs to be signed in some cases in the list of request parameters)

**Generate Pre-sign string**

For following data set：

```
string[] parameters={
  "service=create_forex_trade",
  "partner=2088101568338364",
  "_input_charset=gbk",
  "return_url= http://www.test.com/alipay/return_url.asp",
  "out_trade_no=6741334835157966",
  "subject=test",
  "payment_type=1 ",
  "seller_email=alipay-test01@alipay.com",
  "total_fee=100"
  };
```
  
Rearrange parameters in the data set alphabetically
And connect rearranged parameters with &：

``
_input_charset=gbk&out_trade_no=6741334835157966&partner=2088101568338364&payment_type=1&return_url=http://www.test.com/alipay/return_url.asp&seller_email=alipay-test01@alipay.com&service=create_forex_trade&subject=test&total_fee=100
``

This is the pre-sign string.

<hr/>

**Note:**
 
* Parameters without a value, can be excluded from sign;
* Charset in sign must be consistent with the charset used previously
* If _input_charset is passed, it also shall be signed.
* According to HTTP protocol, special character like &,@ needs to do URL encoding, therefore the request receiver can get correct value. In this situation, pre-sign string shall be the original value instead of encoded one. For example: calling a particular API need to sign the parameter email, the pre-sign string shall be email=test@msn.com, rather than email=test%40msn.com.
<hr/>

### Signature Generation

**MD5 Signature**

Private Key is necessary for MD5 signature. The MD5 private key is the 32-byte string which is composed of English letters and numbers. Partner can log on the Merchant Service Center (https://global.alipay.com) to check the private key.

* Sign for request

After the partner receives the pre-sign string during requesting, the private key should be appended to the pre-sign string to generate the new string. Then this new string would be calculated with the MD5 signature algorithm by the MD5 signature function. Thus, the result 32-byte string is the signature result string. (the value is given to parameter “sign”)  

* Signature Verification for response

After receiving the pre-sign string during responding from Alipay system, the next step is the same as the procedure of Sign for request. When the 32-byte signature result string is generated, it should be verified whether the value is equal to the value of the parameter “sign”. If equal, the verification would be passed.

**DSA, RSA Signature**

Both private key and public key are necessary for DSA or RSA signature. Both private key and public key are generated with OPENSSL by partner. Partner and Alipay need to exchange their own public key. Therefore, partner uses Alipay public key and partner private key.

* Sign for request

After the partner receives the pre-sign string during requesting, the partner private key and the pre-sign string are used in the RSA or DSA signature algorithm by the RSA or DSA signature function to get the result string. (the value is given to parameter “sign”)

* Signature Verification for response

After receiving the pre-sign string during responding from Alipay system, the Alipay public key, the pre-sign string and the parameter “sign” are used in the RSA or DSA signature asymmetric algorithm by the RSA or DSA signature function to accomplish the signature verification.

<br/>

## RSA Key Generation with OpenSSL

### OpenSSL installation

* Linux（Ubuntu）

```
sudo apt-get install openssl
```

* Windows
The developer can download Windows version of OpenSSL from the official site of https://www.openssl.org/source/.

### RSA key pair generation

* Linux

```
$ openssl
  OpenSSL> genrsa -out rsa_private_key.pem 1024 ##generating  private key
  OpenSSL> pkcs8 -topk8 -inform PEM -in rsa_private_key.pem  -outform PEM -nocrypt ##transform private key into PKCS8 format
  OpenSSL> rsa -in rsa_private_key.pem -pubout -out  rsa_public_key.pem ##Generate public key
  OpenSSL> exit         
```

* Windows operates in cmd window:

```
C:\Users\Hammer>cd C:\OpenSSL-Win32\bin ##enter OpenSSL directory
  C:\OpenSSL-Win32\bin>openssl.exe ##enter OpenSSL
  OpenSSL> genrsa -out rsa_private_key.pem 1024  ##generating private key
  OpenSSL> pkcs8 -topk8 -inform PEM -in rsa_private_key.pem  -outform PEM -nocrypt ##transform private key into PKCS8 format
  OpenSSL> rsa -in rsa_private_key.pem -pubout -out  rsa_public_key.pem ##Generate public key
  OpenSSL> exit
```
<hr/>

**Note:**
For Java developers, we need to remove the header, footer, <CR>, and space from the pkcs8 private key output in the console. For.NET and PHP developer, there is no need for the pkcs8 operation.
<hr/>

After the above steps, the user could see two files under the current folder (C:\OpenSSL-Win32\bin for Windows), rsaprivatekey.pem and rsapublickey.pem. 
The former is the private key while the latter is the public key. The merchant should keep the private key and exchange the public key with Alipay for signature verification. The following are the examples on how to use the key pair.

* Standard private key file（PHP,.NET）

```
-----BEGIN RSA  PRIVATE KEY-----MIICXQIBAAKBgQC+L0rfjLl3neHleNMOsYTW8r0QXZ5RVb2p/vvY3fJNNugvJ7lo4+fdBz+LN4mDxTz4MTOhi5e2yeAqx+v3nKpNmPzC5LmDjhHZURhwbqFtIpZD51mOfno2c3MDwlrsVi6mTypbNu4uaQzw/TOpwufSLWF7k6p2pLoVmmqJzQiD0QIDAQABAoGAakB1risquv9D4zX7hCv9MTFwGyKSfpJOYhkIjwKAik7wrNeeqFEbisqv35FpjGq3Q1oJpGkem4pxaLVEyZOHONefZ9MGVChT/MNH5b0FJYWl392RZy8KCdq376Vt4gKVlABvaV1DkapL+nLh7LMo/bENudARsxD55IGObMU19lkCQQDwHmzWPMHfc3kdY6AqiLrOss+MVIAhQqZOHhDe0aW2gZtwiWeYK1wB/fRxJ5esk1sScOWgzvCN/oGJLhU3kipHAkEAysNoSdG2oWADxlIt4W9kUiiiqNgimHGMHPwp4JMxupHMTm7D9XtGUIiDijZxunHv3kvktNfWj3Yji0661zHVJwJBAM8TDf077F4NsVc9AXVs8N0sq3xzqwQD/HPFzfq6hdR8tVY5yRMb4X7+SX4EDPORKKsgnYcur5lk8MUi7r072iUCQQC8xQvUne+fcdpRyrR4StJlQvucogwjTKMbYRBDygXkIlTJOIorgudFlrKP/HwJDoY4uQNl8gQJb/1LdrKwIe7FAkBl0TNtfodGrDXBHwBgtN/t3pyi+sz7OpJdUklKE7zMSBuLd1E3O4JMzvWP9wEE7JDb+brjgK4/cxxUHUTkk592-----END RSA  PRIVATE KEY-----
```

* Standard private key file in PKCS8 format(Java)

```
-----BEGIN PRIVATE  KEY-----MIICeAIBADANBgkqhkiG9w0BAQEFAASCAmIwggJeAgEAAoGBAN0yqPkLXlnhM+2H/57aHsYHaHXazr9pFQun907TMvmbR04wHChVsKVgGUF1hC0FN9hfeYT5v2SXg1WJSg2tSgk7F29SpsF0I36oSLCIszxdu7ClO7c22mxEVuCjmYpJdqb6XweAZzv4Is661jXP4PdrCTHRdVTU5zR9xUByiLSVAgMBAAECgYEAhznORRonHylm9oKaygEsqQGkYdBXbnsOS6busLi6xA+iovEUdbAVIrTCG9t854z2HAgaISoRUKyztJoOtJfI1wJaQU+XL+U3JIh4jmNx/k5UzJijfvfpT7Cv3ueMtqyAGBJrkLvXjiS7O5ylaCGuB0Qz711bWGkRrVoosPM3N6ECQQD8hVQUgnHEVHZYtvFqfcoq2g/onPbSqyjdrRu35a7PvgDAZx69Mr/XggGNTgT3jJn7+2XmiGkHM1fd1Ob/3uAdAkEA4D7aE3ZgXG/PQqlm3VbE/+4MvNl8xhjqOkByBOY2ZFfWKhlRziLEPSSAh16xEJ79WgY9iti+guLRAMravGrs2QJBAOmKWYeaWKNNxiIoF7/4VDgrcpkcSf3uRB44UjFSn8kLnWBUPo6WV+x1FQBdjqRviZ4NFGIP+KqrJnFHzNgJhVUCQFzCAukMDV4PLfeQJSmna8PFz2UKva8fvTutTryyEYu+PauaX5laDjyQbc4RIEMU0Q29CRX3BA8WDYg7YPGRdTkCQQCG+pjU2FB17ZLuKRlKEdtXNV6zQFTmFc1TKhlsDTtCkWs/xwkoCfZKstuV3Uc5J4BNJDkQOGm38pDRPcUDUh2/-----END PRIVATE  KEY-----
```

* Public key file

```
-----BEGIN PUBLIC  KEY-----MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDQWiDVZ7XYxa4CQsZoB3n7bfxLDkeGKjyQPt2FUtm4TWX9OYrd523iw6UUqnQ+Evfw88JgRnhyXadp+vnPKP7unormYQAfsM/CxzrfMoVdtwSiGtIJB4pfyRXjA+KL8nIa2hdQy5nLfgPVGZN4WidfUY/QpkddCVXnZ4bAUaQjXQIDAQAB-----END PUBLIC  KEY-----
```

**Upload the public key**

Contact Global Merchant Technical Support to upload the public key. Please sign with the matching private key in the key pair.
