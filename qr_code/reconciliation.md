## SFTP Connection

The Alipay system has implemented the White List mechanism, and the partner needs to notify Alipay of its public IPs. Then, we will release a username together with password to the partner to test the accessibility and reconciliation file parsing/cron job. If these testings are successful, the partner can push the system to the production.

Alternatively, the partner also can manually access the merchant’s dashboard to download the reconciliation and settlement report, using the the information of below:

URL: https://global.alipay.com

Username: **testoverseas1980@alipay.com** 

Password: **testoverseas1980**

Alipay SFTP Server: **sftp.alipay.com/port:22**

Alipay SFTP Server IP: **110.75.149.86**

The file naming rule is:

1. $PID_transaction_$YYYYMMDD.txt;
2. $PID_settlement_$YYYYMMDD.txt

<br/>

## Transaction File Format

This file consists of two parts: the header and record detail.

**File header**  

The file header contains a list of the following fields (the field names are not showing in the file):

|Occurring sequence in the header	|Field	|Type	|Description|
|-----|-------|-----------| ----------|
|1	|Partner	|String(16)	|2088123456543210|
|2	|Payment_time	|String(10)	|The day that transaction happens, the format is YYYY-MM-DD HH:MM:SS|
|3	|Total_count	|Number(9)	|The total number of the records in this file|
 

**Record Detail**

|No.	|Field	|Type(Byte)	|Description|
|-----|-------|-----------| ----------|
|1	|Partner_transaction_id	|String(64)	|A numbered transaction ID(unique in partner system)it is equal to “partner_trans_id” when transaction type is in (payment,reversal,reverse); it is equal to “partner_refund_id” when transaction type is refund|
|2	|Transaction_id	|String(64)	|A numbered transaction ID （Unique inside the Alipay system）|
|3	|Transaction_amount	|Number(9,2)	|Same to the definition given in the interface part;<br/>It is in the currency given below.|
|4	|Charge_amount	|Number(9,2)	|Commission fee|
|5	|Currency	|String(8)	|The currency given in the transaction request.|
|6	|Payment_time	|String(19)	|The time of transaction;<br/>Format: YYYY-MM-DD HH:MM:SS|
|7	|Transaction_type	|String(8)	|Transaction type：<br/>PAYMENT<br/>REVERSE<br/>REFUND|
|8	|Remark	|String(256)	|Remark|
|9	|Secondary_merchant_industry	|String(4)	|Industry classification identifier|
|10	|Secondary_merchant_name	|String	|Secondary merchant name (or a taxi company name)|
|11	|Operator_name	|String	|Operator name (store name field)|
|12	|Order_scene	|String	|Order scenarios:<br/>Scan QR code mode : shopQrCode<br/>Barcode mode: It is blank|
|13	|Trans_currency	|String(8)	|List currency|
|14	|Trans_amount	|Number(9,2)	|Amount in list currency/refund amount in list currency|
|15	|Trans_forex_rate	|String	|Exchange rate of list currency against settlement currency|

An example of file content:

Partner:208800000000|Payment_time: 2013-12-02|Total_count:4

Partner_transaction_id|Transaction_id|Transaction_amount|Charge_amount|Currency|Payment_time|Transaction_type|Remark|Secondary_merchant_industry|Secondary_merchant_name|Operator_name|Order_scene|Trans_currency|Trans_amount|Trans_forex_rate

0001|201312020445|100|3|HKD|2013-12-02 10:45:42|PAYMENT||5812|xxx|xxx|shopQrCode|TWD|100|0.031

0002|201312020446|100|3|HKD|2013-12-02 10:45:13|REVERSAL||5812|xxx|xxx|shopQrCode|TWD|100|0.031

0003|201312020447|100|3|HKD|2013-12-02 10:45:56|CANCEL||5812|xxx|xxx|shopQrCode|TWD|100|0.031

0004|201312020448|100|3|HKD|2013-12-02 10:45:09|REFUND|Refund|5812|xxx|xxx|shopQrCode|TWD|100|0.031
