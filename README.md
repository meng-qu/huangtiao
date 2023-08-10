This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.js`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to automatically optimize and load Inter, a custom Google Font.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.


# 小黄条项目 —— 让小宝贝的小黄条不再满天飞

## 技术框架
1. 全栈Nextjs
2. 数据库用MongoDB 登入用ssl安全证书 确保登入时的保密性
3. 用户验证用Google Oauth2.0
4. 部署用Vercel

## 前端功能
1. 首次登录的用户需要注册 
2. 成功登陆后的用户界面有上下两个区域
   + 上部区域有添加功能 用来输入六个值：App名称 用户名 密码 注册邮箱 密码回答问题的答案 备注
   + 下部显示目前所有已添加项目 其中密码部分用*遮盖 点击小眼睛才能睁眼看到
      - 对于已添加的项目 旁边都有可修改icon小铅笔 点击后可修改指定字符

## 后端及数据库结构
1. 用户注册时 用户名密码记录在MongoDB的users Collection
   + 从Users Collection 调用密码字符串作为后续加密所用的Key
   + 从Users Collection 调用用户名字符串创建新的Collection
2. 在Node中使用Axios的call back函数 调用key值 存储在session cookie
3. 在每一次session开始时 验证用户登录的有效性
4. 从数据库找到对应用户Collection 用GET读取readall 记录
5. 用户进行添加、更新、删除操作时：
   + 在前端进行GET,POST,PUT 时 调取key进行加密
     - PUT需要数据库运行find 
   + 在前端进行DELETE时 不需要key介入 弹出提示对话框
     - 在数据库运行delete
6. session每60分钟自动revoke
