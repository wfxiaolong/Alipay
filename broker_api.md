<p align="center"><img src="alipay.png">
<h3 align="center">IE Money -- Alipay Broker Document</h3><hr>
</p>

```
IE MONEY Alipay is the best way to access the chinese customers purse.
```

#### USAGE:

* Step 1: Register **Broker Account** from our managers.
* Step 2: Intergrate in your platform. (API)

#### Protocol:

**Interface**

```
Method: HTTP POST

https://mypay.iemoney.co.nz/api/getSubTransaction

Params:
username       // [string] required
password       // [string] required
start_date     // [string] option   eg. "1991-11-26"
end_date       // [string] option   eg. "2017-11-26"
per_page       // [int]    option   eg. 10
start_with     // [int]    option   eg. 0
merchant_id    // [int]    option   eg. 10001 

```

```
Example:

Call:
https://mypay.iemoney.co.nz/api/getSubTransaction

Post data:
"username" => "username",
"password" => "12323213",
"per_page" => "2",
"start_with" => "0",
"merchant_id" => "10001",
"start_date" => "2017-08-16",
"start_date" => "2017-08-16"

Result:
{
    "is_success": "TRUE",
    "message": "SUCCESS",
    "extra": {
        "broker": {
            "id": "1",
            "username": "horton",
            "account_manager": "xiaolong",
            "account_manager_contact": "12313232",
            "commission_rate": "1.6",
            "contact_phone": "1591321321",
            "contact_email": "1231@gmial.com",
            "location": "auckland",
            "balance": "0",
            "bank_account_number": "bank_nmufdfa",
            "bank_account_holdername": "xlong_bank",
            "last_ip": "127.0.0.1",
            "last_logintime": "2017-10-16 10:46:17",
            "superuser": "Y",
            "broker": "Y"
        },
        "sub_merchant": [
            {
                "loginname": "eris",
                "id": "10001"
            },
            {
                "loginname": "wanguo",
                "id": "10003"
            }
        ],
        "total": "42",
        "transactions": [
            {
                "id": "4356",
                "merchant_id": "10001",
                "currency": "NZD",
                "amount": "1.11",
                "customer_name": "150****1605",
                "alipay_trans_id": "2017081621001004080502xxxxxxx",
                "partner_trans_id": "2017081615331868173705591834xxxxx",
                "payment_status": "P",
                "settle_status": "S",
                "refund_status": "Y",
                "payment_time": "2017-08-16 15:33:18",
                "settle_time": "2017-09-21 14:21:06",
                "refund_time": "2017-08-16 16:51:41",
                "loginname": "eris",
                "commission_rate": "2.0"
            },
            {
                "id": "4355",
                "merchant_id": "10001",
                "currency": "NZD",
                "amount": "1.00",
                "customer_name": "150****1605",
                "alipay_trans_id": "2017081621001004080xxxx26xxxx",
                "partner_trans_id": "312307443083150285421xxxx",
                "payment_status": "P",
                "settle_status": "S",
                "refund_status": "Y",
                "payment_time": "2017-08-16 11:30:13",
                "settle_time": "2017-09-21 14:21:06",
                "refund_time": "2017-08-16 16:51:37",
                "loginname": "eris",
                "commission_rate": "2.0"
            }
        ]
    }
}

```

##### Result:

We can get payment result from the website directly. Synchronize.







