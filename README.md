# Worldpay SDK

Worldpay SDK for **orders** calls.

# Requirements

Python 2.7 or Python 3.6+

# Installation

```bash
pip install worldpay
```

# Usage

## Things you will need

At minimum, you'd need to have a Worldpay account (a test account will do). With the account you'll receive a **service key** which will be needed to authenticate yourself when making calls and a **client key** used to when providing card details to Worldpay.

Once you have these, you can setup your Worldpay config:

```python
from worldpay.worldpay import Worldpay

Worldpay.WORLDPAY_SERVICE_KEY = 'Your Worldpay Service Key'
```

## Generating a Token

Prior to making a Orders request, it is necessary to get a token from Worldpay using your client key. This should be done on the client side of your application using worldpay.js. See [TestingPays ](https://github.com/TestingPays/worldpay_python_example_app) for a detailed example.

### Orders Request

To create an orders request, pass the generated token, along with the amount, currency code and a description to the create_charge function as shown below.

```python
  response = Worldpay.create_charge(
        token=request.POST['worldpayToken'],
        amount=request.POST['amount'],
        order_description = 'My order description',
        currency_code = request.POST['currency']
    )
```

A successful response object will be a dict, containing status code, order code and the message

```python

{
  "status_code": 200,
  "message": "SUCCESS",
  "order_code": "db6f616a-08c5-11e7-8fd4-b8e8564628bc"
}

```

Responses other than http code of 200 will be a dict containing a status code and a message

```python

{
  "status_code": 400,
  "message": "INVALID_PAYMENT_DETAILS"
}

```
