<p align="center"><img src="alipay.png">
<h3 align="center">MYPay -- Alipay Check Offline Payment</h3><hr>
</p>

``
MYPay Alipay is the best way to access the Chinese customers purse. 
``

#### USAGE:

* Step 1: Regist account from our managers. <a href="https://mypay.tech">https://mypay.tech</a>
* Step 2: Intergrate Offline Payment API in your platform.
* Step 3: Intergrate this API in your platform.

#### Protocol:

**Interface**

```
Method: HTTP GET

https://mypay.iemoney.co.nz/api/check_offline_payment/$alipay_trans_id

OR

https://mypay.iemoney.co.nz/api/check_offline_payment/$partner_trans_id
```

|Parameter	|Type 	|Description|
|-----------|-------|-----------|
|alipay_trans_id     |int |Order ID|
|partner_trans_id    |int |Order ID|

<br/>


```
Example:

https://mypay.iemoney.co.nz/api/check_offline_payment?alipay_trans_id=2017121821001004130232299311

```

#### Result:

Customers can get the payment result that if it is successful or not.


