# 目录

[toc]



## Ewas机器备份

```
10.11.104.136   dev
10.11.104.135   qa
10.11.104.137   stg
```



## Ewas 压测环境







## tenant服务走跳板机快速部署

```
#stg
scp /home/lab_admin/tmp/bbtest/rtm-tenant-http-0.0.1-SNAPSHOT-exec.jar   safetysuite@10.11.104.137:/home/safetysuite/data/cluster/bbtest/     

#qa
scp /home/lab_admin/tmp/bbtest/rtm-tenant-http-0.0.1-SNAPSHOT-exec.jar   safetysuite@10.11.104.135:/home/safetysuite/data/cluster/bbtest/


#临时文件夹tenant 替换
cp  /home/safetysuite/data/cluster/bbtest/rtm-tenant-http-0.0.1-SNAPSHOT-exec.jar  ../cluster/


#重启tenant
sudo service ss-app_tenant  restart
```

