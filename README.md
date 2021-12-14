# 用 AWS CDK 我也可以一鍵上傳前端網站
[![Gitpod Ready-to-Code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/clarencetw/gitpod-cdk-web)

## 安裝環境
### 安裝 AWS CLI
- `python3 -m pip install --no-input --upgrade awscli`

### 安裝 AWS CDK CLI
- `npm install -g aws-cdk`

### 在 Gitpod 設定 AWS CLI KEY
```
eval $(gp env -e AWS_ACCESS_KEY_ID=XXXXXXXXX)
eval $(gp env -e AWS_SECRET_ACCESS_KEY=YYYYYYY)
eval $(gp env -e AWS_DEFAULT_REGION=ZZZZZZZZ)
```

### 測試 AWS CLI
- `aws sts get-caller-identity`

## 創建 CDK v1 專案
- `mkdir cdk-frontend-web && cd cdk-frontend-web`
- `npx projen new awscdk-app-ts`

### 新增 projen CDK 模組
```
deps: [
  "@aws-cdk/aws-s3",
  "@aws-cdk/aws-s3-deployment"
],
```

### 撰寫程式
#### 使用 CDK v1 方法 import
```
import * as s3 from '@aws-cdk/aws-s3';
import * as s3deploy from '@aws-cdk/aws-s3-deployment';
```

## 創建 CDK V2 專案
- `mkdir cdk-frontend-web && cd cdk-frontend-web`
- `npx projen new awscdk-app-ts --cdk-version 2.1.0`

### 撰寫程式
#### 使用 CDK v2 方法 import
```
aws_s3 as s3f
aws_s3_deployment as s3deploy
```

## 新增要部署的靜態網站
- `npx @vue/cli create --default website`
- `cd website`
- `yarn build`

## 新增程式到 MyStack
### 創建 S3 Bucket
```
const destinationBucket = new s3.Bucket(this, 'WebsiteBucket', {
    websiteIndexDocument: 'index.html',
    publicReadAccess: true,
    removalPolicy: RemovalPolicy.DESTROY,
    autoDeleteObjects: true,
});
```

### 設定 S3 Deployment
```
new s3deploy.BucketDeployment(this, 'HTMLBucketDeployment', {
    sources: [s3deploy.Source.asset('./website/dist')],
    destinationBucket,
    prune: true,
});
```

### 顯示 S3 Website URL
```
new CfnOutput(this, 'bucketWebsiteUrl', {
    value: destinationBucket.bucketWebsiteUrl,
});
```

## 部署
### 首次執行
- `cdk bootstrap`

### 部署 CDK 專案
- 直接部署 `cdk deploy`
- 直接部署不經過檢查 `cdk deploy --require-approval`
- 一邊撰寫一邊部署 `cdk watch`

### 移除部署
- `cdk destroy`
