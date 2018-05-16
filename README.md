# coreos-esxi
Container Linux Config on ESXi 

1. 将 Container Linux Config 转为 Ignition，使用 base64 编码
```
( ct -platform openstack-metadata -in-file config.clc | base64 -w0 - ) && echo
```

2. 登陆 ESXi 宿主机，手动编辑虚拟机 .vmx 文件，添加配置
```
guestinfo.coreos.config.data.encoding = "base64"
guestinfo.coreos.config.data = 
```
注：vCenter/ESXi 管理界面，右键虚拟机->编辑设置->选项->高级->常规->配置参数，可以添加 guestinfo.<property> 配置，但配置的值长度有限制。
