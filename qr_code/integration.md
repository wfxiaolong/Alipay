## Integration Overview

Throughout the integration, whenever the merchant system intends to interact with the Alipay system for a specific service, it needs to send an HTTPs request to the corresponding interface. Upon receiving the request, the Alipay system will first verify the request; if the verification is successful, then the Alipay system will respond the result data to the merchant server.

To integrate a merchant’s system with Alipay to run the Merchant QR Code payment solution, a typical merchant basically needs to implement the functions to generate the merchant’s QR Code, reverse, refund a transaction, which will be respectively explained in this section.

<br/>

## Create Flow

<p align="center">
    <img alt="Parcel" src="img/qr_qi1.png" width="80%">
</p>

A merchant can request to generate a QR Code to permanently represent its counter in this Merchant QR Code Payment solution, and the Figure 3 illustrates the work flow. For this flow, we would like to highlight:

1. The merchant can request to generate a static QR code by this interface “alipay.commerce.qrcode.create” (CREATE), and it is important to note that this interface requires to input a “notification URL”, to which Alipay will send a notification with transaction status after a successful payment 
2. The parameter values for calling the precreate service are encapsulated in the first HTTPs request data, including the signature related data;
3. The CREATE service request will fail if either the signature is invalid or other compulsory parameter values are absent or illegal;
4. For the full list of parameters and values of the CREATE service, please refer the corresponding interface API for detail.

<br/>

## Pay Flow

<p align="center">
    <img alt="Parcel" src="img/qr_qi2.png" width="80%">
</p>

In the context of the Merchant QR Code payment, the QR Code permanently represent the mechant’s conter. Thus, whenever a customer needs to pay an order, the customer just needs to scan the QR Code to input the amount to pay and then confirm the payment, and the Alipay will send a notification then.

Upon receiving the notification of a payment from Alipay, the merchatn should verify the signature and validate the information sent back in the notification with the customer’s payment details. 

<br/>

## Cancel Flow

<p align="center">
    <img alt="Parcel" src="img/qr_qi3.png" width="80%">
</p>

During the payment process of a transaction, it is possible to encounter issues such as system exception or network accessibility. In such a scenario, you need to reverse the transaction. To implement this reversing, we would like to highlight the notes of below:

1. In this integration, please use the CANCEL to reverse a transaction, and the interface name is: alipay.acquire.cancel;
2. For a transaction that has been successfully paid, the CANCEL is able to refund the transaction within the transaction day (GMT+8).;
3. Comparing with the REFUND service, if a transaction can be refunded by this CANCEL interface, the transaction fee that hass been charged by Alipay will always be refunded as well;
4. For a transaction has encountered technical issues during making the payment, the CANCEL is able to roll back all the actions have been performed in the Alipay system regarding the specific transaction;
5. For the full list of parameters and error code of this CANCEL service, please refer the interface API document for details. 

<br/>

## Refund Flow

<p align="center">
    <img alt="Parcel" src="img/qr_qi4.png" width="80%">
</p>

For a transaction that has been successfully paid, the customer can request the merchant for refunding as long as the refunding period is still valid, and the merchant can make use of the refunding interface to complete the refunding, as illustrated.

For the integration of the refunding service, we woulkd like to highlight:

1. The refunding service name is: alipay.acquire.overseas.spot.refund(REFUND);
2. To refund a transaction, the interface REVERSE is only applicable at the same day of the payment (GMT +8, Beijing time); on the other hand, the interface REFUND is applicable as long as the refunding period has not expired yet;
3. the refunding of a transaction can be full or partial, i.e. the refunding amount can respectively be the same as or less than the original transaction amount that has been paid; furthermore, for a transaction, multiple refunding request is allowed provided the sum of the amount of the multiple refunding request is less than or equal with the original transaction amount. 

<br/>

## Testing Credentials

To enable the testing when you develop the integration, we provide an official account, and the specifics are:

     Partner ID (PID): **2088021966388155**

      MD5 Key value: **w0nu2sn0o97s8ruzrpj64fgc8vj8wus6**

The RSA private key is:

```
-----BEGIN RSA PRIVATE KEY (For PHP)-----
MIICXAIBAAKBgQD7FfmVdd570cFX3G76FatugmYlGNFtw9b2kFiBPvJDM0yeX52S
WqAtjVBizaf6zNzib1a9xety7dnAxELidQJmUj3z4lwb3j5PRn+lx5FeAyAJWRBS
m5+J3AzhOoHpStgATvEXT/AUndrgdn5Adfi45koUB8IzJzGZmk+5DabrIwIDAQAB
AoGABd2WjgpJ30SgKqhIo2j8L0G2lylEQzcu/2WR27sXt8AsCwsayD97vHSvqw84
3GAKzPNi6F4GSRILYzhyg43ON3/d3m/S1iTgSFXchTyAsAjy398Iq/ufSj9DOj+u
I88XZ7JVt7jEyihPldSh7FkuMKaaFkJdsNz22LfD3NZIBVECQQD+I/zp+OuxmW5D
GcNDEIXF0bl3mmCAv041ZBBO5JCYrgvpkofC6SRlOi+P3BPXYPHZjyU3Jp3XgaJD
QvHCEkXbAkEA/OxD8FDM5i1JqcwIzha+NyJdm3nJ7Njlx4VIKD9Kx10oG49ge7gG
8fDC7FwduGupfPj9ycKsHBFWC+AIUPSGWQJASqzWbwWWc+wKiyrxxi3/sL3MSomR
G6Oa3nNVm2jr2AEkPPCydaI98ISlXxciuWGiDvRR0h/Ft4I+5JayJP1riwJAHe6o
K6ykUylQ6nNnJ1yxrjy270t+hjU1HGO9omW7J9TyhjB1rq6cw81GhEpyifzT1iJx
hosvazLyB/2/fjUyIQJBAJDzo5n2tVhsQEe5aNlF5ZHTtReyTMnPR4HgfBqGWydc
DV/Wx7roFLX0dYT71CMD3vvHtda0qfNpQe8nM43lJfc=
-----END RSA PRIVATE KEY-----
```

```
----BEGIN RSA PRIVATE KEY (For JAVA)-----
MIICdgIBADANBgkqhkiG9w0BAQEFAASCAmAwggJcAgEAAoGBAPsV+ZV13nvRwVfcbvoVq26CZiUY0W3D1vaQWIE+8kMzTJ5fnZJaoC2NUGLNp/rM3OJvVr3F63Lt2cDEQuJ1AmZSPfPiXBvePk9Gf6XHkV4DIAlZEFKbn4ncDOE6gelK2ABO8RdP8BSd2uB2fkB1+LjmShQHwjMnMZmaT7kNpusjAgMBAAECgYAF3ZaOCknfRKAqqEijaPwvQbaXKURDNy7/ZZHbuxe3wCwLCxrIP3u8dK+rDzjcYArM82LoXgZJEgtjOHKDjc43f93eb9LWJOBIVdyFPICwCPLf3wir+59KP0M6P64jzxdnslW3uMTKKE+V1KHsWS4wppoWQl2w3PbYt8Pc1kgFUQJBAP4j/On467GZbkMZw0MQhcXRuXeaYIC/TjVkEE7kkJiuC+mSh8LpJGU6L4/cE9dg8dmPJTcmndeBokNC8cISRdsCQQD87EPwUMzmLUmpzAjOFr43Il2becns2OXHhUgoP0rHXSgbj2B7uAbx8MLsXB24a6l8+P3JwqwcEVYL4AhQ9IZZAkBKrNZvBZZz7AqLKvHGLf+wvcxKiZEbo5rec1WbaOvYASQ88LJ1oj3whKVfFyK5YaIO9FHSH8W3gj7klrIk/WuLAkAd7qgrrKRTKVDqc2cnXLGuPLbvS36GNTUcY72iZbsn1PKGMHWurpzDzUaESnKJ/NPWInGGiy9rMvIH/b9+NTIhAkEAkPOjmfa1WGxAR7lo2UXlkdO1F7JMyc9HgeB8GoZbJ1wNX9bHuugUtfR1hPvUIwPe+8e11rSp82lB7yczjeUl9w==
-----END RSA PRIVATE KEY-----
```

The RSA Alipay public key is:

```
-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCnxj/9qwVfgoUh/y2W89L6BkRAFljhNhgPdyPuBV64bfQNN1PjbCzkIM6qRdKBoLPXmKKMiFYnkd6rAoprih3/PrQEB/VsW8OoM8fxn67UDYuyBTqA23MML9q1+ilIZwBC2AQ2UBVOrFXfFl75p6/B5KsiNG9zpgmLCUYuLkxpLQIDAQAB
-----END PUBLIC KEY-----
```

<br/>

## Demo Code Download

Payment: Merchants can reference the following alipay demo code to do quick integration or directly check the API document and construct the http request to make the payment.

**Demo Code Download**
|Language         |	MD5              |	RSA            |
| --------------- |------------------| ----------------|
|JAVA	            |<a href="https://os.alipayobjects.com/rmsportal/cvVqqhhjVWIlJbZIshhs.zip">download</a>	|<a href="https://os.alipayobjects.com/rmsportal/lmxfxSsEnyOMFjMlyYfw.zip">download</a>|
|PHP	            |<a href="https://os.alipayobjects.com/rmsportal/NcZcaCyNGpCRYRuHCydU.zip">download</a>|<a href="https://os.alipayobjects.com/rmsportal/dQqStmcIYYkTkriYcMmJ.zip">download</a> |
|.Net	            |<a href="https://os.alipayobjects.com/rmsportal/GcdhgHgXAgQjcoCVGCHo.zip">download</a>|<a href="https://os.alipayobjects.com/rmsportal/DIZvNQwshHAbOoFVsQjB.zip">download</a>|
<br/>
