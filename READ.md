# Integrate Cognito, API Gateway and Festivus API

## Requirements
* Registed and approved users can use our Festivus API after they sign in. Their sign in status will be expired after X minutes.
* We will provide REST API to customer and we want to decouple the request URL and the real resources address.

## Solution
Using Amazon API Gateway to decouple user requests URL and realy resource address.  
Using JWT to authenticate valid user.
Using Amazon Cognito as our authorization service which will create JWT for valid user.  

## Why API Gateway
Festivus already has REST APIs which can be called. So, the only thing we need to do is decouple.  
The common way of decouple is add a layer "in front of" our Festivus API.   
Images
Amazon API Gateway not only act as the "front door" for applications to access data, but also very easy for developer to publish, maintain, monitor, and secure APIs.  

## Why JWT
Session, JWT and other tech all can do the thing of keep user's authrization status.   
JWT has one key advantage: decouple the authrization service and application service.  
Using JWT, we have two different type services: authorization service and application service. 
On the application service, we don't need any storage to store session info or user login info. 
More over, we can using third part auth service.  

### JWT signature
* Create JWT head and payload
* Hash Code = SHA-256(base64url(head) + "." + base64url(payload))
* Digital Signature = RSA_Encode(Hash Code, Private Key)
* JWT = base64url(head) + "." + base64url(payload) + "." + Digital Signature  

### JWT verify
* decoded_hash_code = RSA_decode(JWT.signature, Public Key)
* hash_code = SHA-256(JWT.head + "." + JWT.payload)
* If hash_code == decoded_hash_code means this JWT string is created/sent by the private key owner and head and payload data has not be modified.  

## Why Cognito
* Decouple
* Safe
* Simple

