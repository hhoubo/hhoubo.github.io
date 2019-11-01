---
layout: single
title:  "Set up google cloud endpoints"
date:   2019-10-28 10:51:23 +0900
categories: serverless
tags: cloud serverless
---
## 要解决的问题
写了很多cloud function 但都要处理CORS, authention等common问题.
通过设置api gateway去解决多处重复配置的问题.

## Set up Cloud Endpoints
1. Select a project and enable the Endpoints feature
    - 会创建一个Developer Portal
    - 生成一个Portal url

2. Edit the openapi.yaml configuration
    - [set up the CORS](https://cloud.google.com/endpoints/docs/openapi/specify-proxy-startup-options#adding_cors_support_to_esp)

3. 使用`cloud shell` 或者Google cloud SDK to deploy the openapi.   
`gcloud endpoints services deploy {YOUR_OPENAPI_CONFIG.yaml}`

### To use Endpoints for OpenAPI
- Configure Endpoints
- Deploy the Endpoints configuration
- Deploy the API Backend

### access controll and Authenticating API users
LAP具有一个单独的账户serviceAPI, LAP user通过firebase验证后使用LAP的服务账户对API进行调用. 当发布API之后,API user 可以申请API key来直接调用.

### cloud function or app engine as API backend
1. Unit of dpeloyment:  application or function
2. Driven by Cloud or Firebase envents
![Choose the serveless platform](https://cloud.google.com/images/serverless-options/serverless-guide.svg)

Cloud Function | App Engine 
---------------|-----------  
simple | complex
small piece | project 
load/restore | access ready 
function | application
For running code that responds to real-time events, or for serving requests without containers, use Cloud Functions.|For when you need multiple pieces of functionality in a single place and want to just deploy your entire application, look to App Engine.

## Reference
1. [Getting started with Endpoints for Cloud Functions](https://cloud.google.com/endpoints/docs/openapi/get-started-cloud-functions)
2. [Compare Cloud Run, Cloud Functions, App Engine](https://www.signalfx.com/blog/gcp-serverless-comparison/)
