# Introduction

Charge& is a platform where users can earn or collect kilometers when using services of our partners (e.g. buying products through partner online shops).
As kilometers are the currency of the Charge& platform, users can spend them on using services of our partners (e.g. paying for a charging session).

A set of APIs is available to all Charge& partners to enable partners to use and consume services. Those services and APIs are described within the subsequent sections.

## Services offered

Currently live Charge& services are:
- [__Charge&Pay__](charge_and_pay.md#chargepay) - pay for a charging session with Charge& kilometers
- [__Charge&Picture__](charge_and_pictures.md#chargepictures) - take a picture of a charging location and get rewarded with kilometers

## Technical details

Services are offered as REST API endpoints in general.
The endpoints exchange requests and responses in JSON format.
The APIs are available for backend integration. Each partner who wants to consume Charge& APIs needs to register as a partner with Charge&.
During [__partner registration__](setting_up.md) an access token is provided to the partner which will be used in subsequent communication.

After successfull registration of a partner, all APIs require the access token to be presented within the Authorization header of the request as a Bearer token.

