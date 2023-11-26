# ElasticSearch

--------------

## 参考资料
[课程教案](/ElasticSearch/ELK课程教案.pdf)

[参考文档](https://www.kuangstudy.com/bbs/1354069127022583809)

[ElasticSearch](https://www.elastic.co/cn/downloads/elasticsearch)

###  安装踩坑

+ 不能安装到 root 用户下
+ 在用户 bash 下设置 JAVA_HOME 环境变量
+ Ubuntu 下切换 Java 版本
    + `sudo update-alternatives --config java`
+ 虚拟内存不能太小
    + sysctl -a|grep vm.max_map_count   // 查看
    + sysctl -w vm.max_map_count=262144 // 设置

### 可视化工具
[Kibana](https://www.elastic.co/cn/downloads/kibana)
M1 Mac 8.12未支持

---
## 分词插件
[ik](https://github.com/medcl/elasticsearch-analysis-ik)

### 1、踩坑

nginx 配置浏览器显示 dic 扩展文件中的中文

```nginx
# ik 分词远程词典库
server {
    listen   8092;              # 端口
    server_name 10.211.55.2;    # 暴露 IP

    charset utf-8;              # 可识别的字符集
    root    /Users/hanwenhao/Documents/ik词库; # 分词库路径
    location / {
        index  index.html index.htm; # 默认入口

        ## 处理扩展名为 dic txt 的文件
        if ($request_filename ~* ^.*?\.(dic|txt)$) {
            add_header Content-Disposition: attachment;           # 是否预期在浏览器中内联显示 是
            add_header Content-Type "text/plain; charset=utf-8";  # 设置响应头为 text 以展示未知的 dic 类型文件
        }
    }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   html;
    }
}
```

### 2、分词语法
```json
GET _analyze
{
    "analyzer": "ik_smart",     // 最少切分(你好世界作为一个分词)
    "text": "你好世界"
}

GET _analyze
{
    "analyzer": "ik_max_word",  // 最细粒度(能拆多少是多少 这时候会参考 *.dic 分词文件)
    "text": "是一句话"
}
```

---
## 集群界面工具
[elasticsearch-head](https://github.com/mobz/elasticsearch-head)

### 1、踩坑
elasticsearch 配置文件需要配合设置跨域

### 2、Rest Api

#### 1) 类比 SQL
+ bool
    + must     : and
    + should   : or
    + must_not : not
+ filter(range)
    + gte      : >
    + lte      : <
+ tags

#### 2) API 文档

[API 文档](https://www.knowledgedict.com/tutorial/elasticsearch-api.html)

[Java 客户端](https://www.elastic.co/guide/en/elasticsearch/client/java-api-client/current/connecting.html)

