Initiate a Transaction via Server-Side API
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

Generating Authorization (using cURL JSON API POST)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| 

.. raw:: html

   <div class="terminal-wrap">

::

    curl https://acs.vds.com.ng/transaction/auth \
    -H "Authorization: Merchant HASH_KEY" \
    -H "Content-Type: application/json" \
    -d '{"transaction":{"accountNo":"0688258274","memo":"Payment For 1 Book","reference":"029882","amount":"100","currency":"USD","type":"sale","return_url":"https://mywebsite.com/thanks.html","notify_url":"https://mywebsite.com/notify.aspx","customer":{"name":"Martin Luther","email":"martinluther@testmail.xxx","phone":"+448002566955"}}}' \
    -X POST

.. raw:: html

   </div>

To calculate the HASH_KEY, its the sha512 hasing of accountNo,
reference, amount and API Key. Your Merchant API Key will be issued to
you.

Result Format
~~~~~~~~~~~~~

| 

.. raw:: html

   <div class="terminal-wrap">

::

    {
      "status": true,
      "message": "Authorization URL created",
      "data": {
        "authorization_url": "https://acs.vds.com.ng/vpc/0peioxfhpn",
        "access_code": 

.. raw:: html

   </div>

.. _demo merchant details provided here: start-testing
