# Linking your users to &Charge users

As a partner you can access the &Charge API with a system user. This user authenticates you as a partner and authorizes you to do requests on behalf of your users.
To use one of your users with any of the &Charge services this user must be linked to a &Charge account.
To do so, the following process is required to link your account with a &Charge user:
1. You send us a request to our [__accounts endpoint__](link_partner_account.md#setting-up-an-account-link). This will initiate the process of linking accounts. To complete the linking of your user accounts with Charge&, you'll need to direct your user from your UI to ours with the activation code encoded within the link.
2. Present a text explaining that the accounts will be linked to your user along with a [__link to our mobile Apps or web page__](app_deep_links.md). This link has to contain the activation code again.
3. Once the user clicks on that link he'll be prompted to login with his/her &Charge account (if not already logged into Charge&). After the user is logged into Charge&, the &Charge app or web page will finalize the account link with the &Charge backend. In case the user does not have a &Charge account yet, account registration can be done prior to accepting the link.

## How to link to us

From within your UI design a screen that tells your user that he is about to link his account with his &Charge account.
Provide a button or link to the user which leads to the following URL when clicked:

| Method      | URL                                                                                                                                                                  | Environment                          
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| GET         | https\://and-charge.com/#/confirmAccountLink?activationCode\=**(code)**&partnerId=**(partnerId)**&partnerUserId=**(partnerUserId)**&callbackUrl=**(callbackUrl)**    | Production
| GET         | https\://pp.and-charge.com/#/confirmAccountLink?activationCode\=**(code)**&partnerId=**(partnerId)**&partnerUserId=**(partnerUserId)**&callbackUrl=**(callbackUrl)** | Pre Production

Fill the place holders according to the following table:

| Placeholder      | Description                          
|------------------|------------------------------------------------------------|
| (code)           | The activation code you got as a result of calling [__accounts endpoint__](link_partner_account.md#setting-up-an-account-link) to start the linking process
| (partnerId)      | The partnerId you chose during [__registering your system__](partner_registration.md#api-endpoint-partner-registration) as a partner of Charge&
| (partnerUserId)  | The user ID you gave us with the request to obtain the activation code.
| (callbackUrl)    | The URL to which we should redirect the user after completion of the account linking. Please URL encode this URL before passing it along.

The user will then be presented the &Charge UI. This will either direct the user to our web page or, if already installed, to the &Charge App. There the user has to register or login and confirm the link. Once confirmed, our UI will direct the user back to the callback URL you provided. The callback URL will contain query parameters reporting on the success of the operation.
You can find the status of the operation with the query parameter "ok" (true representing an established link while false indicates an error). In case of an unsucessful operation, the query parameter error will have one of the following values:

| Value                            | Description                          
|----------------------------------|------------------------------------------------------------|
| MANDATORY_PARAMETER_NOT_SET      | Your request was missing a mandatory parameter. Please check the URL.
| ACCOUNT_LINKED_TO_DIFFERENT_USER | The user behind partnerUserId is already linked to a different user of Charge&
| PARTNER_NOT_FOUND                | We did not recognize the partnerId. Either your registration is not yet finished or something else is wrong. Inform us, we'll figure it out.
| GENERAL_PROCESSING_FAILURE       | Something went wrong on our side. Please get in touch with us, we'll have a look into it. If our backend is unable to process this request, giving it a try a bit later could also solve this.
| ACTIVATION_CODE_NOT_FOUND        | We did not recognize the activation code you gave us, make sure you use the one, you got from calling our [__accounts endpoint__](link_partner_account.md#setting-up-an-account-link).

## How to remove the link between your user and &Charge again 
In case the user does not want the link between the accounts anymore, there is an [__API to remove the link__](link_partner_account.md#removing-an-account-link) available.