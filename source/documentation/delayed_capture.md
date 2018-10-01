GOV.UK Pay supports the delayed capture of payments.

To use this feature, include `"delayed_capture": true` in the body of a [create new payment](https://gds-payments.gelato.io/api-explorer/gov-uk-pay-api/versions/1.0.2/general/create-new-payment) request (link opens in new window). 

The user experience matches the current payment flow. Once the user selects __Confirm__ on the __Confirm your details__ page, your service can call the `POST /v1/payments/{paymentId}/capture` endpoint to send a delayed capture request.

There are 4 possible responses:

<div style="height:1px;font-size:1px;">&nbsp;</div>

| Response Code  | Meaning                    |
| -------------- | -------------------------- |
|204             | Capture request accepted   |
|404             | `paymentId` does not exist |
|409             | Capture request rejected   |
|500             | Downstream error           |

<div style="height:1px;font-size:1px;">&nbsp;</div>

Your service must send the delayed capture request within 90 minutes of the payment creation, regardless of how long the user takes to complete the payment flow. Otherwise, it will expire.

If your service has enabled payment receipt emails, GOV.UK Pay will send a payment receipt email to the user once your service's capture request is received and accepted.