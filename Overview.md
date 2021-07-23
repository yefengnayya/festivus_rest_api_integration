# Integrate Cognito, API Gateway and Festivus API

## Requirements
* Registed and approved users can use our Festivus API after they sign in. Their sign in status will be expired after X minutes.
* We will provide REST API to customer and we want to decouple the request URL and the real resources address.

## Solution
Using JWT to authenticate valid user.  
Using Amazon Cognito as our authorization service which will let user, sign in and create JWT for valid user.  
Using Amazon API Gateway to decouple user requests URL and realy resource address.  
Component diagram:  
![Component Diagram](images/component.png?raw=true)

## Why API Gateway
The common way of decouple is add a layer "in front of" our Festivus API.   
Amazon API Gateway can act as the "front door" for applications to access data and very easy for developer to publish and maintain.  
Easy integrate with Cognito.  

## Why JWT
Session and JWT all can do the thing of keeping user's authrization status. However, JWT has a key advantage: decouple service.  
Using JWT, we can decouple authorization service and application service.  
On the application service side, we don't need to store session info or user login info. The only thing we will do is check the validation of JWT's signature.  
On the authorization service side, it will store the user's info, authenticate and create JWT.  
We can using third party authorization service: Congito.  

### Why JWT can decouple services
RSA is assymmetic algorithm. It has public/private key pair.  
If we use a private key to encrypt some thing, only the public key which matchs the private key can decrypt it.  
Authorization service is the owner of private/public key pair. Public key is published and  private key is secret.  
If app service can decrypt data by the authorization service's public key, it means that data must be encrypted by authorization service's private key. Because authorization service is the only owener of the private key, so the data must come from authorization service.


### JWT signature
* Create JWT head and payload
* Hash Code = SHA-256(base64url(head) + "." + base64url(payload))
* Digital Signature = RSA_Encript(Hash Code, Private Key)
* JWT = base64url(head) + "." + base64url(payload) + "." + Digital Signature  

### JWT verify
* decoded_hash_code = RSA_decript(JWT.signature, Public Key)
* hash_code = SHA-256(JWT.head + "." + JWT.payload)
* If hash_code == decoded_hash_code means this JWT string is created/sent by the private key owner and head and payload data has not be modified.  


## Why Cognito
Cognito contain all things we need for the authenticate and authorizeation.  
User sign up, sign in, create token.   
Easy integrate to other aws service.  
If MAU(Month activate user) less 50,000, it is free.  


## Authenticate and Authorization workflow:  
![Component Diagram](images/sequence-1.png?raw=true)  


## Improvement
Sequence diagram:  
![Component Diagram](images/sequence-2.png?raw=true)  