# 用 AWS CDK 我也可以一鍵上傳前端網站

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
- `aws sts get-caller-identity --no-cli-pager`

## 創建專案
- `mkdir cdk-frontend-web && cd cdk-frontend-web`
- `npx projen new awscdk-app-ts`