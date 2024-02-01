# docker

docker container update --restart=always 容器名字

docker ps: 查看容器信息

### bili 动态rss

```bash
docker run -d --name rsshub -p 1200:1200 -e CACHE_EXPIRE=3600 -e BILIBILI_COOKIE_692655144="SESSDATA=818fb0cc%2C1708957982%2Cc07f3%2A81CNj7T5tXuSmdHyjKXwvaiHpoxzPPkyZxsnXhLbUmkNZE9-X3GiCKUXqMsJ427LAX-KXJKQAALAA;" diygod/rsshub
```

http://188.34.165.110:1200/bilibili/followings/dynamic/692655144

参考：https://docs.rsshub.app/zh/install#%E9%83%A8%E5%88%86-rss-%E6%A8%A1%E5%9D%97%E9%85%8D%E7%BD%AE