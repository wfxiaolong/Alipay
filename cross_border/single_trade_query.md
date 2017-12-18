
<p align="center"><img src="/alipay.png">
<h3 align="center">MYPay -- Alipay Check Offline Payment</h3><hr>
</p>

```
MYPay Alipay is the best way to access the Chinese customers purse.

The partners can use this API to obtain the information on transaction status.
```

#### Protocol:

**Interface**

```
Method: HTTP GET

https://mypay.iemoney.co.nz/api/check_offline_payment

```

|Parameter	|Type 	|Description|
|-----------|-------|-----------|
|partner_trans_id    |varchar(32) |Order ID (optional)|

<br/>


```
Example:

https://mypay.iemoney.co.nz/api/check_offline_payment?alipay_trans_id=2017121821001004130232299311

```

#### Result:

Customers can get the payment result that if it is successful or not.


