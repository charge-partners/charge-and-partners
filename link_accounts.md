# Linking your users to Charge& users

As a partner you can access the Charge& API with a system user. This user authenticates you as a partner and authorizes you to do requests on behalf of your users.
To use one of your users with any of the Charge& services this user must be linked to a Charge& account.
To do so, the following process is required to link your account with a Charge& user:
1. You send us a request to our [__accounts endpoint__](link_partner_account.md#setting-up-an-account-link). This will initiate the process of linking accounts. For this you will need the activation code sent to you within the response of that request.
2. Present a text explaining that the accounts will be linked to your user along with a link to our iOS app or web page. This link has to contain the activation code again.
3. Once the user clicks on that link he'll be prompted to login with his/her Charge& account (if not already logged into Charge&). After the user is logged into Charge&, the Charge& app or web page will finalize the account link with the Charge& backend. In case the user does not have a Charge& account yet, account registration can be done prior to accepting the link.

In case the user does not want the link between the accounts anymore, there is an [__API to remove the link__](link_partner_account.md#removing-an-account-link) again.