## Transaction File Format

### Record Detail

|No.	|Field	|Type(Byte)	|Description|
|-----|-------|-----------| ----------|
|1	|Partner_transaction_id |String(64)	|The unique transaction ID specified by the partner. If the id is duplicated with an earlier transaction’s out_trade_no, the payment will fail with a error message indicating that it is the duplicated payment. It is equal to “out_trade_no” in the payment request when the transaction type is 'P'.|
|2	|Transaction_id	|String(64)	|Alipay Transaction ID.Max length is 64 and min length is 16.|
|3	|Amount	|Number(8,2)	|The amount foreign currency given.|
|4	|Rmb_amount	|Number(8,2)	|The amount RMB currency given.|
|5	|Fee	|Number(8,2)	|Commission fee in foreign currency|
|6	|Distribute_amount	|String(8,2)	|This trade's split foreign currency amount or this refund's split refund foreign currency amount.|
|7	|Distribute_rmb_amount	|String(8,2)	|This trade's split RMB amount or this refund's split refund RMB amount.|
|8	|Settlement	|String(8,2)	|The amount of foreign settlement currency|
|9	|Rmb_settlement	|String(8,2)	|The amount of RMB settlement currency|
|10	|Currency	|String(10)	|The settlement currency code the merchant specifies in the contract.|
|11	|Rate	|String(8,6)	|The exchange rate.|
|12	|Payment_time	|String(19)|The time of transaction;<br/> Format: YYYY-MM-DD HH:MM:SS|
|13	|Settlement_time	|String(19)	|The time of settlement;<br/> Format: YYYY-MM-DD HH:MM:SS|
|14	|Type	|String(1)	|Normal transaction: P <br/> Refund transaction: R|
|15	|Status	|String(1)	|Normal transaction: <br/> P: Payment made <br/> L: Liquidated <br/> Refund transaction: <br/> F: Failed <br/> L: Liquidated
|16	|Remarks	|String(256)	|Remarks|

**An example of file content:**

Partner_transaction_id|Transaction_id|Amount|Rmb_amount|Fee|Distribute_amount|Distribute_rmb_amount|Settlement|Rmb_settlement|Currency|Rate|Payment_time|Settlement_time|Type|Status|Remarks
GDR-EP-5729068-20170927105445022|2017092721001003000000578434|2899.05|2473.73|34.79|0.0|0.0|2864.26|2444.04|HKD|0.85329000|2017-09-27 10:57:23||P|P|GDR-EP-5729068-20170927105445022
FOREXREFUND_2017092700641633|2017092721001003720000000258|555.0|473.58|6.66|0.0|0.0|548.34|467.9|HKD|0.85329000|2017-09-27 21:37:08||R|P|GDR-EP-5727442-20170927144456087

<br/>

## Settlement File Format

### Record Detail

|No.	|Field	|Type(Byte)	|Description|
|-----|-------|-----------| ----------|
|1	|Partner_transaction_id	|String(64)	|The unique transaction ID specified by the partner. If the id is duplicated with an earlier transaction’s out_trade_no, the payment will fail with a error message indicating that it is the duplicated payment. It is equal to “out_trade_no” in the payment request when the transaction type is 'P'.|
|2	|Transaction_id	|String(64)	|Alipay Transaction ID.Max length is 64 and min length is 16.|
|3	|Amount	|Number(8,2)	|The amount foreign currency given.|
|4	|Rmb_amount	|Number(8,2)	|The amount RMB currency given.|
|5	|Fee	|Number(8,2)	|Commission fee in foreign currency|
|6	|Distribute_amount	|String(8,2)	|This trade's split foreign currency amount or this refund's split refund foreign currency amount.|
|7	|Distribute_rmb_amount	|String(8,2)	|This trade's split RMB amount or this refund's split refund RMB amount.|
|8	|Settlement	|String(8,2)	|The amount of foreign settlement currency|
|9	|Rmb_settlement	|String(8,2)	|The amount of RMB settlement currency|
|10	|Currency	|String(10)	|The settlement currency code the merchant specifies in the contract.|
|11	|Rate	|String(8,6)	|The exchange rate.|
|12	|Payment_time	|String(19)	|The time of transaction;<br/> Format: YYYY-MM-DD HH:MM:SS|
|13	|Settlement_time	|String(19)	|The time of settlement;<br/> Format: YYYY-MM-DD HH:MM:SS|
|14	|Type	|String(1)	|Normal transaction: P<br/> Refund transaction: R|
|15	|Status	|String(1)	|Normal transaction:<br/> L: Liquidated<br/>Refund transaction:<br/>L: Liquidated|
|16	|Remarks	|String(256)	|Remarks|

**An example of file content:**

Partner_transaction_id|Transaction_id|Amount|Rmb_amount|Fee|Distribute_amount|Distribute_rmb_amount|Settlement|Rmb_settlement|Currency|Rate|Payment_time|Settlement_time|Type|Status|Remarks
GDR-EP-5542324-20170922110026136|2017092221001000000009179004|0.01|0.01|0.0|0.0|0.0|0.01|0.01|HKD|0.84682000|2017-09-22 11:04:13|2017-09-28 15:36:00|P|L|GDR-EP-5542324-20170922110026136
GDR-EP-5542324-20170922110729211|2017092221001000000009204295|0.01|0.01|0.0|0.0|0.0|0.01|0.01|HKD|0.84682000|2017-09-22 11:11:05|2017-09-28 15:36:00|P|L|GDR-EP-5542324-20170922110729211
