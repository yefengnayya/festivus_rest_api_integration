# How to Do
## Create Cognito User Pool
* Login to AWS Coginto console
* Click 'Manage User Pools'
* Click 'Create a user pool'
* Input Pool name and click 'Step through settings'
Most attributes we can use default setting. Few attributes we need to pay attention.
### App clients setting
* Add App client name
* Config token expiration
* Check all in 'Auth Flows Configuration'
* We will use 'App client id' and 'App client secret' in our code
### App integration
* 'Resource server' add the api gateway URL to Identifier
  
  

## Create API in API Gateway
### Create API
* Login to AWS API Gateway Console
* Click 'Create API'
* Select 'REST API' type
* Input  API name

### Create Resource
* Open 'API recource' page 
* In 'Actions' dropdown, click  'Create Resource'
* Input resouce name and click 'Create Resource'

### Create Method
* Click the resource that we just created
* In 'Actions' dropdown, click 'Create Method'
* In dropdown, select method we want to create
* Select integration type
* Click 'Save'
* In the mothod detail page, we can config the request headers, query string parameters etc.

### Create Authorizer
* In the left menu of API, click 'Authorizers'
* Click 'Create new Authorizer'
* Input name, type(select 'Cognito'), Cognito User Pool name, Token Source

### Add author to method
* Back to the API method page
* Click 'Method Request'
* Set 'Authorization' the the Authorizaton we just created
* Add 'email' to 'OAuth Scopes'

### Deoloy API
* In 'Actions' dropdown, click 'Deploy API'
* In 'Deployment stage' create or select stage
* In the left side menu, click 'Stages'
* Find 'Invoke URL' of the API resource. This URL is the end point URL of REST API.
  


