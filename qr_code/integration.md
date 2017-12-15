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


