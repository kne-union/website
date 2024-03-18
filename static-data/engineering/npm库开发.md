1. 使用脚手架初始化项目

```shell
npx create-react-app libName --template=@kne/cra-template-lib
```

2. 初始化示例程序

```shell
npm run init-example
```

3. 按照README.md修改项目对应项

4. 启动项目

```shell
npm run start 
```

5. 完成示例和文档

6. 提交到github，合并到master后action自动发布版本

7. 如果需要将示例文档集成到[kne-union ued](https://kne-union.github.io/ued)
   中，需要在 [ued-manifest](https://github.com/kne-union/ued-manifest)的package.json中添加配置

```json
{
  "ued-config": {
    "libs": [
      "npm 包名"
    ]
  }
}
```
