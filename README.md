# Cloudflare Demo

## 测试 Worker 和 D1

```sh
npm init -y
npm add wrangler -D

npx wrangler init
npx wrangler d1 create demo_db

# 查看数据库信息，填写到 toml 文件
npx wrangler d1 list

# 设计表，并在本地创建
npx wrangler d1 execute demo_db --local --file=./schema.sql
# 验证，应输出 table
npx wrangler d1 execute demo_db --local --command='SELECT * FROM Comments'

# 开发 npm run dev
# failed to run
npx wrangler dev --local --persist

# 部署，去掉 local
npx wrangler d1 execute demo_db --file=./schema.sql
# 同步到远端数据库
npx wrangler d1 execute demo_db --remote --file=./schema.sql

npx wrangler deploy
```
## 获取所有评论
```
https://cloudflare-demo.xxxxxx.workers.dev/api/comments
```
## 获取特定昵称的评论
```
https://cloudflare-demo.xxxxxx.workers.dev/api/comment?nickName=mgl
```

## 添加评论
```
curl -X POST -d '{"content":"quick test","nickname":"mgl"}'  https://cloudflare-demo.xxxxxx.workers.dev/api/comment/add
```
