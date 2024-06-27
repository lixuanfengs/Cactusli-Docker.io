

# Cactusli-Docker.io：Docker 官方镜像代理工具

基于 Cloudflare Workers 的 Docker 镜像代理工具。此工具能够中转对 Docker 官方镜像仓库的请求，有效解决访问限制并加速镜像下载。

## 部署方式

- **Workers** 部署：复制 [_worker.js](https://github.com/cmliu/CF-Workers-docker.io/blob/main/_worker.js) 代码，`保存并部署`即可
- **Pages** 部署：`Fork` 后 `连接GitHub` 一键部署即可

## 如何使用？

例如您的Workers项目域名为：`cactusli.xxx.net`；

### 1.官方镜像路径前面加域名
```shell
docker pull cactusli.xxx.net/stilleshan/frpc:latest
```
```shell
docker pull cactusli.xxx.net/library/nginx:stable-alpine3.19-perl
```

### 2.一键设置镜像加速
修改文件 `/etc/docker/daemon.json`（如果不存在则创建）
```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://cactusli.xxx.net"]  # 请替换为您自己的Worker自定义域名
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 变量说明
| 变量名 | 示例 | 必填 | 备注 |
|--|--|--|--|
| URL302 | https://cactusli.xxx.net |❌| 主页302跳转 |
| URL | https://www.baidu.com/ |❌| 主页伪装(设为`nginx`则伪装为nginx默认页面) |

