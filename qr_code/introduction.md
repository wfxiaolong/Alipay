## Introduction

### The Product

The Merchant QR Code Payment solution is making use of a static QR code to represent the account of a merchant. In this payment solution, the customer needs to scan the QR code and then input the amount to complete the payment.

To provide such a payment service, one solution is that the merchant integrates with Alipay system through the interfaces that have been developed for this product.

### The Alipay Service

To achieve the integration of Merchant QR Code Payment, you need to make use of the following Alipay services:

* alipay.commerce.qrcode.create (CREATE).<br/>
This servisce is able to create a QR code to represent the merchant account.

* alipay.commerce.qrcode.modify (MODIFY).<br/>
Merchants can modify the merchant QR code that is generated by the QR code creation interface.

* alipay.commerce.qrcode.modifyStatus (MODIFYSTATUS).<br/>
By using the QR code status modification inferface, the QR code can be stopped, restarted, or deleted.

* alipay.acquire.overseas.spot.refund (REFUND).<br/>
This interface provides the ability to refund a transaction either fully or partially provided it is within the refundable period.

* alipay.acquire.overseas.query (QUERY).<br/>
This service enables the merchant to query a transaction’s status by these two parameters, partner_trans_id and alipay_trans_id.

* alipay.acquire.cancel (CANCEL).<br/>
This interface serves to completely roll back a transaction within the transaction day(GMT+8), which can be successfully completed or not.
