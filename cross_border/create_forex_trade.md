<p align="center"><img src="/alipay.png">
<h3 align="center">MY PAY -- Alipay Online Document</h3><hr>
</p>

``
MY PAY Alipay is the best way to access the chinese customers purse.
``

#### USAGE:

* Step 1: Regist account from our managers. <a href="https://mypay.tech">https://mypay.tech</a>
* Step 2: Configure Your Callback URL.(Synchronize And Asynchronize) <a href="https://mypay.tech">https://mypay.tech</a>
* Step 3: Intergrate in your platform.

#### Protocol:

**Interface**

```
Method: HTTP GET

https://mypay.iemoney.co.nz/api/onlinePayment/$mid/$subject/$price/md5($mid.$subject.$price.$api_key)/$order_no
```

|Parameter	|Type 	|Description|
|-----------|-------|-----------|
|mid        |int |merchant id, Get from the backstage|
|subject    |string  |describe payment|
|price      |string  |otal to pay|
|api_key    |string  |get from the backstage|
|order_no   |string  |order number, identify the order (optional)<br/>Tips: trade_no = random_string('numeric', 16)|

All of the params should use urlencode.

<br/>

```
Example:

Call:
https://mypay.iemoney.co.nz/api/onlinePayment/10209/IE_PRODUCT/1.00/aacda3da67342a0961faa7c631041871/2017080808080808

Callback Synchronize:
http://callbackURL.com/2017080808080808/TRADE_FINISHED

Callback Asynchronize:
http://callbackUrl.com/2017080808080808/TRADE_FINISHED/aacda3da67342a0961faa7c631041871

http://callbackUrl.com/$tradeNo/$status/md5($tradeNo.$status.$api_key)

```

##### Result:

We can get payment result from the website directly. Synchronize.
But the only right way to judge is to access our backstage or asyn callback. And you can also receive an Email.


