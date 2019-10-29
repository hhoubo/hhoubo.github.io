---
layout: single
title:  "Set up google cloud endpoints"
date:   2019-10-28 10:51:23 +0900
categories: serverless
tags: cloud serverless
---
## 要解决的问题
写了很多cloud function 但都要处理CROS, authention等common问题.
通过设置api gateway去解决多处重复配置的问题.

## Set up Cloud Endpoints
1. Select a project and enable the Endpoints feature
    - 会创建一个Developer Portal
    - 生成一个Portal url

2. Edit the openapi.yaml configuration
    - [set up the CORS](https://cloud.google.com/endpoints/docs/openapi/specify-proxy-startup-options#adding_cors_support_to_esp)

3. 使用`cloud shell` 或者Google cloud SDK to deploy the openapi.   
`gcloud endpoints services deploy {YOUR_OPENAPI_CONFIG.yaml}`

## Reference
1. [Getting started with Endpoints for Cloud Functions](https://cloud.google.com/endpoints/docs/openapi/get-started-cloud-functions)
