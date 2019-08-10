# Win10 Docker Desktop镜像挂载问题

Docker Desktop 版本 2.1.0.1

挂架Docker镜像中的路径至Win10本地路径

提示错误invalid bind mount source must be an absolute path

现在记录正确的挂载写法，version > 3.3, 挂载本地目录使用/host_mnt/盘符/目录(或文件)

```yml
version: "3.3"
services:
  portainer:
    image: portainer/portainer:1.22.0
    command: --no-auth
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /host_mnt/e/portainer:/data
    ports:
      - target: 9000
        published: 9000
        protocol: tcp
        mode: host
    networks:
      - test-net
      
networks:
  test-net:
    external: true
```

