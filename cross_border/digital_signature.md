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
<br/>

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
