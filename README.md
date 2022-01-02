# README

AWS CDKの練習用

### 環境
```
Ruby3
M1 Mac
```

# 開発環境

```
$ docker-compose up
```

# 本番環境
### デプロイ

```
$ cd aws-cdk-ecs-on-fargate-sample
$ cdk deploy
```

### ECRにイメージのpush
#### app

```
$ cd rails6-sample-app
$ aws ecr get-login-password --region ap-northeast-1 | docker login --username AWS --password-stdin [accountID].dkr.ecr.ap-northeast-1.amazonaws.com
$ docker build -f ./ecs/Dockerfile . -t aws-cdk-ecs-on-fargate-sample-app --platform linux/amd64
$ docker tag aws-cdk-ecs-on-fargate-sample-app:latest [accountID].dkr.ecr.ap-northeast-1.amazonaws.com/aws-cdk-ecs-on-fargate-sample-app:latest
$ docker push [accountID].dkr.ecr.ap-northeast-1.amazonaws.com/aws-cdk-ecs-on-fargate-sample-app:latest
```

#### nginx

```
$ cd rails6-sample-app/nginx
$ aws ecr get-login-password --region ap-northeast-1 | docker login --username AWS --password-stdin [accountID].dkr.ecr.ap-northeast-1.amazonaws.com
$ docker build -f ./nginx/Dockerfile -t aws-cdk-ecs-on-fargate-sample-nginx . --platform linux/amd64
$ docker tag aws-cdk-ecs-on-fargate-sample-nginx:latest [accountID].dkr.ecr.ap-northeast-1.amazonaws.com/aws-cdk-ecs-on-fargate-sample-nginx:latest
$ docker push [accountID].dkr.ecr.ap-northeast-1.amazonaws.com/aws-cdk-ecs-on-fargate-sample-nginx:latest
```

### リソースの削除

```
$ cd aws-cdk-ecs-on-fargate-sample
$ cdk destroy
```

※ destroyでECRのリポジトリとCloudWatch Logsのロググループは削除されないため手動で削除が必要
