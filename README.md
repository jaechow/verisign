# VeriSign Payflow Pro API SDK #

VeriSign Payflow Pro is a high performance TCP/IP-based Internet payment
solution. Payflow Pro is pre-integrated with leading e-commerce solutions and is
also available as a downloadable software development kit (SDK).
Payflow Pro is multi-threaded and allows multiple concurrent transactions from a
single client. It can be integrated as a Web-based or a non-Web-based application.
It does not require the HTTP protocol to run, which allows for greater flexibility in
configuration and reduced processing overhead for higher performance.

### How Payflow	Pro Works ###
Payflow Pro uses a client/server architecture to transfer transaction data from you
to the processing networks, and then returns the authorization results to you.
Payflow Pro can process real-time credit card, ACH, or check transactions to most
of the financial processing centers in the United States.

1. The Payflow Pro client encrypts each transaction request using the latest Secure Sockets Layer (SSL) encryption and establishes a secure link with the VeriSign processing server over the Internet.
2. The VeriSign server, a multi-threaded processing environment, receives the request and transmits it (over a secure private network) to the appropriate financial processing network for real-time payment authorization.
3. The response (approved/declined, and so on) is received from the financial network and is returned via the same session to the Payflow Pro client.
4. The Payflow Pro client completes each transaction session by transparently sending a transaction receipt to the VeriSign server before disconnecting the session.

The entire process is a real-time synchronous transaction.  Once connected, the transaction is immediately processed and the answer returned in about three seconds.  Payflow Pro does not affect or define the time periods of authoirzations, nor does it influence the approval or denial of transactions.

When integrating with Payflow pro, you need only be concerned with passing all the required data for transaction authorization.  the settlement (close batch) operation is handled by VeriSign.


## Performing Credit Card Transactions ##
### Credit Card Transaction Format ###
>**Note** The examples in this section use the syntax of the `pfpro` executable client.  Other Payflow Pro clients differ in where and how the parameter values are set, but the meaning and uses are the same.
Use the following syntax when calling the Payflow Pro client `pfpro` to process a transaction.

```
pfpro <HostAddress> <HostPort> "<ParmList>" <TimeOut> <ProxyAddress> <ProxyPort> <ProxyLogon> <ProxyPassword>
```

For example:
```pfpro test-payflow.verisign.com 443
"TRXTYPE=S&TENDER=C&PARTNER=verisign&VENDOR=SuperVendor&USER=tester&PWD=x1y2z3&ACCT=5499740000000016"&EXPDATE=0822&AMT=123.00"
```

>Arguments to the pfpro executable client

|Argument 	|Required 	|Description|
|:----------|:----------|:----------|
|**HostAddress**|Yes    |VeriSign's host name.  For testing use **test-payflow.verisign.com**.  For live transactions, use any IP address in the range **216.168.252.0 to 216.168.252.20.**|
|**HostPort**|Yes       |Use port 443|
|**ParmList**|Yes       |The ParmList is the list of parameters that specify the payment information for the transaction.  The quotation marks "" at the beginning and end are required.  In the example, the ParmList is ```"TRXTYPE=S&TENDER=C&PARTNER=verisign&VENDOR=SuperVendor&USER=tester&PWD=x1y2z3&ACCT=5499740000000016"&EXPDATE=0822&AMT=123.00"``` The content of the ParmList varies by the type of transaction being processsed.  For example, a Void transaction requires a different set of parameters than does a Sale transaction.|
|**TimeOut** |Yes   |Time-out period for the transaction.  The minimum recommended time-out value is 30 seconds.  The VeriSign client begins tracking from the time that is sends the transaction request to the VeriSign server.|
|**ProxyAddress\***|No  |Proxy server address   |
|**ProxyPort\*** |No   |Proxy server port   |
|**ProxyLogon\***|No   |Proxy server logon ID|
|**ProxyPassword\***|No|Proxy server logon password|

>\*Use these parameters for servers behind a firewall.  Your network administrator can provide these values.


