VdsPay API Documentation

Getting Started
====================

This document will show you how to get up and running with VdsPay. The
API is a comprehensive and RSESTFUL HTTP API that enhances communication
between your application and vdspay

Transactional Queries

-  `Initiate a Transaction via Server-Side API`_\ (Recommended)
-  `Initiate a Transaction via Simple HTML`_
-  `Query Transaction`_
-  `Receive Payments(Bitcoin)`_

Account Queries

-  `Check Balance`_
-  `Transfer To VdsPay Account`_
-  `Send BitCoin`_

Other Instructions

-  `Currency Converter`_

For additional support, please email Acquiring@vds.com.ng

.. _: index.html
.. _Initiate a Transaction via Server-Side API: #authorization-server-side
.. _Initiate a Transaction via Simple HTML: #authorization-html
.. _Query Transaction: #requery
.. _Receive Payments(Bitcoin): #bitcoin
.. _Check Balance: #balance
.. _Transfer To VdsPay Account: #transfer
.. _Send BitCoin: #send_bitcoin
.. _Currency Converter: #currency


Authorization(Server-Side)
~~~~~~~~~~~~~~~~~~~~

Integrating VdsPay with an existing website is easy and can be achieved
with simple steps.

At a high level you want to achieve the following:

-  ** POST transaction details to Obtain Authorization URL
-  ** Calculate a request hash to ensure transaction integrity
-  ** Provide a URL which VdsPay would post back the authorization
   response
-  ** Query the transaction details directly from VdsPay to ensure the
   actual transaction amount was approved

The only requirement is to **POST** transaction data to the **VdsPay**
server via JSON API. The section below describes how to create this
**POST** with cURL.



.. raw:: html



   <div class="st-alert st-alert-success">


.. rubric:: Heads up!
   :name: heads-up


You can now use the \ `demo merchant details provided here`_ to start
testing your code and integration immediately without completing the
sign up process.


.. raw:: html


   </div>
   
| 

.. raw:: html

   <div class="terminal-wrap">
   
::

    curl https://acs.vds.com.ng/transaction/auth \
    -H "Authorization: Merchant HASH_KEY" \
    -H "Content-Type: application/json" \
    -d '{"transaction":{"accountNo":"0688258274","memo":"Payment For 1 Book","reference":"029882","amount":"100","currency":"NGN","type":"sale","return_url":"https://mywebsite.com/thanks.html","notify_url":"https://mywebsite.com/notify.aspx","customer":{"name":"Martin Luther","email":"martinluther@testmail.xxx","phone":"+448002566955"}}}' \
    -X POST

.. raw:: html

   </div>
   
To calculate the HASH_KEY, its the sha512 hashing of accountNo, reference, amount and API Key. Your Merchant API Key will be issued to you.

Result Format


| 

.. raw:: html

   <div class="terminal-wrap">

::

    {
      "status": true,
      "message": "Authorization URL created",
      "data": {
        "authorization_url": "https://acs.vds.com.ng/vpc/0peioxfhpn",
        "access_code": "0peioxfhpn" } }
		
.. raw:: html

   </div>

.. _demo merchant details provided here: #start-testing


Authorization(Html)
~~~~~~~~~~~~~~~~~~~~

A deprecated integration in HTML is available for soft programmers. WE DO NOT RECOMMEND THIS! 


.. raw:: html

   <div class="terminal-wrap">

::

    <form class="form-horizontal" role="form" method="POST" action="https://acs.vds.com.ng/webscr/?cmd=_pay" target="_top">
      <input type="text" name="customer_phone" value="2340000000000">
      <input type="hidden" name="ref_code" value="0000000">
      <input type="hidden" name="memo" value="Transaction Testing"/>
      <input type="hidden" name="return_url" value="https://mywebsite.com">
      <input type="hidden" name="tn_type" value="sale"> 
      <input type="hidden" name="acct_number" value="00000">
       <input type="hidden" name="amount" value="100.00">
    <input type="hidden" class="form-control" name="customer" value="John Doe">
          <input type="hidden" name="customer_email" value="shshs@ok.k">
          <select name="currency">
          <option value="NGN">NGN</option>
          </select>
          <button type="submit" class="btn btn-default">Submit</button>
    </form>

.. raw:: html

   </div>
