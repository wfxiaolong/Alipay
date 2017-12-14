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
