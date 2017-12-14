<p align="center"><img src="alipay.png">
<h3 align="center">MY PAY -- Alipay Offline Document</h3><hr>
</p>

```
MY PAY Alipay is the best way to access the chinese customers purse.
```

#### USAGE:

* Step 1: Regist account from our managers.
* Step 2: Intergrate in your platform.

#### Protocol:

**Interface**

```
Method: HTTP PSOT

https://mypay.iemoney.co.nz/api/scan_barcode

Data:
userame        // [string] username
barcode        // [string] scan barcode
item           // [string] name for item
price          // [string] total to pay
hasRate		   // [int] 0,1 是否包含了费率, 1 表示包含了.直接扣用户这么多钱.

```

##### Result:

```
if (res.data.is_success == "TRUE")     // 直接支付成功了<br/>
if (res.data.message == "FAIL_PAY")    // 需要用户点击确认...需要轮训查询订单交易是否成功<br/>
else  // 请求失败
```

We can get payment result from the website directly. Synchronize.
But the only right way to judge is access our backstage. And you will also receive an Email.




