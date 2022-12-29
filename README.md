### 容器化部署:
1. Npm run build对项目进行打包，生成dist文件夹。
2. 把项目复制到nginx的默认目录下。
3. 编写dockerfile：
```
FROM nginx:alpine
ADD ./ /usr/share/nginx/html/
EXPOSE 80
```
4. 构建镜像
```
docker build . -t myTodo-image
```
5. 创建docker容器
```
docker run -d -p 88:80 --name myTodo-container myTodo-image:latest
```

### 项目预览:
![alt 属性文本](https://i.postimg.cc/9Q2cDpk8/add.jpg)
![alt 属性文本](https://i.postimg.cc/43NZ53sp/done.jpg)
![alt 属性文本](https://i.postimg.cc/0yCPDSR8/clear.jpg)
