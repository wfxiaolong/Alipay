## Integration Overview

Throughout the integration, whenever the merchant system intends to interact with the Alipay system for a specific service, it needs to send an HTTPs request to the corresponding interface. Upon receiving the request, the Alipay system will first verify the request; if the verification is successful, then the Alipay system will respond the result data to the merchant server.

To integrate a merchant’s system with Alipay to run the Merchant QR Code payment solution, a typical merchant basically needs to implement the functions to generate the merchant’s QR Code, reverse, refund a transaction, which will be respectively explained in this section.


## Create Flow

<p align="center">
    <img alt="Parcel" src="img/qr_qi1.png" width="80%">
</p>

A merchant can request to generate a QR Code to permanently represent its counter in this Merchant QR Code Payment solution, and the Figure 3 illustrates the work flow. For this flow, we would like to highlight:

1. The merchant can request to generate a static QR code by this interface “alipay.commerce.qrcode.create” (CREATE), and it is important to note that this interface requires to input a “notification URL”, to which Alipay will send a notification with transaction status after a successful payment 
2. The parameter values for calling the precreate service are encapsulated in the first HTTPs request data, including the signature related data;
3. The CREATE service request will fail if either the signature is invalid or other compulsory parameter values are absent or illegal;
4. For the full list of parameters and values of the CREATE service, please refer the corresponding interface API for detail.
