# 用 AWS CDK 我也可以一鍵上傳前端網站

## 安裝環境
### 安裝 AWS CLI
- `brew install awscli`

### 安裝 AWS CDK CLI
- `brew install aws-cdk`

### 設定 AWS CLI
- `${GITPOD_REPO_ROOT}/utils/refresh_credentials.sh`

### 測試 AWS CLI
- `aws sts get-caller-identity --no-cli-pager`

## 創建專案
- `mkdir cdk-frontend-web && cd cdk-frontend-web`
- `npx projen new awscdk-app-ts`