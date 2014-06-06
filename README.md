<p align="left"><a href="http://apigee.com/" style="font-size:25px;font-family:Lucida Sans Unicode"><img src="http://apigee.com/about/sites/all/themes/apigee_themes/apigee_mktg/images/logo.png"/> Grass</a></p>

Overview
--------
[Grass](grass-definition) is an identity solution based on Apigee Edge platform. Identity is building block any digital ecosystem needs, be it either it is application, data analysis and contextual content delivery through APIs.

Key difference between Grass and traditional identity system are:

    •   It can handle millions of users 
    •   It is exposed as REST API and Standards (Open ID Connect)
    •	It has in-built consent mgmt., expandable for all non-identity resource type as well
    •	It can authenticate using different mechanism including SMS Login, Social login etc.
    
The identity solution is built based upon the OpenID Connect 1.0 specification. The spec is is a simple identity layer on top of the OAuth 2.0 protocol. Check the details at [OpenID connect](http://openid.net/connect/) and [FAQ](http://openid.net/connect/faq/). The FAQ has a nice 5 minute video, don't miss to check it out.
The solution at present supports the [Authorization Code flow](http://openid.net/specs/openid-connect-core-1_0.html#CodeFlowAuth). It does not support [Implicit](http://openid.net/specs/openid-connect-core-1_0.html#ImplicitFlowAuth) and [hybrid](http://openid.net/specs/openid-connect-core-1_0.html#HybridFlowAuth) flows. 



Architecture and API Specification
----------------------------------

<p align="left"><a><img src="https://i.cloudup.com/55Lv-NK4H2.png"/></a></p>

Broadly the present Architecture can be modularised as follows:

#### Apps
   * Consent App
     * Consent Managment solution on Apigee Edge. 
     * Supports the Demo app for Consent Management.
   * Demo App
     * Demonstrates the Identity solution. 
     * Accepts User Login, Mobile phone Login, Social login.
     * Presently only User Login is implemented. 
     * Upon successful user authentication, asks for User consent.
     * Post user allowing consent, shows user location information to mark completion.

#### API's
   * Internal
     * Identity-Authentication-spi
        * Wrapper for Thrid party Identity service provider interface. 
        * Presently not used. 
        * Contributions required.
     * Identity-sms-token-api
        * Provide SMS token capabilities for Strong authentication
        * [Details](https://github.com/apigeecs/grass/blob/master/docs/source/index.md)
   * External
     * Identity-Consentmgmt-api
        * Provides Consent Management support on Apigee Edge. 
        * Uses App Services to store consent. Custom collections - consent, sso
        * [Details](https://github.com/apigeecs/grass/blob/master/docs/source/consent-management-api.md)
     * Identiy-Usermgmt-api
        * The identity provider API. 
        * Uses App Services as the User store. Default collection - user
        * [Details](https://github.com/apigeecs/grass/blob/master/docs/source/index.md)               
     * Identity-oauthv2-api
        * The key identity API based upon the OpenID spec.
        * Presently supports only the authorization code flow. 
        * [Details](https://github.com/apigeecs/grass/blob/master/docs/source/identity-api.md)
            


Deploying and Using Identity Solution
-------------------------------------
Pre-Requisite:
You need to have access to deployed Apigee Edge Services with organization details. If you don’t have this – please sign-up at [Edge](http://enterprise.apigee.com)

    Git clone “grass” repo
    Goto /grass/src/gateway/setup-identity. 
    Run setup.sh
    
	The setup script prompts for your organization on Apigee Edge, the environment to setup the Identity solution and Edge credentials 
	
	It then creates API service resources ( cache resources) ,  a developer (Identity User),  product ( Identity App product) and a app ( Identity App) for the created developer. 

	It prompts again for App services organization (by default an app services org exists for your org on Edge, so this can be used) and name for the App to be created on App services. 

	Post this, the App services is setup along with 2 custom collections (Consent & SSO). 

	In the end it deploys the Identity API Proxies to your specified org and deploys to your specified env.

###### Please Note: 
The setup.sh needs to be executed from setup-identity folder. It would fail otherwise since relative paths are used from the setup-identity folder. Please feel free to contribute to the setup script itself and make it robust.

###### Grass Definition
Grasses are critical building block for food chain.. It used in many forms as lawns, food(rice, wheat etc), beverages(beer, whisky etc) and feeding animal. 
