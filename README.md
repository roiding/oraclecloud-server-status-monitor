# Oracle Cloud Always Free 服务器状态监控
### 本项目建议有一定编程经验者使用
忘了从何时开始，甲骨云开始会不定时周期性的把不长具有活跃性的服务器关停。

**本项目主要监控服务器运行状态，在甲骨文云关停时，自动通过oci进行启动。**

## 使用步骤：
在secrets中填写如下几个变量(确保操作以下内容时已经登陆oraclecloud，多租户的人别找我)
1. REGION

截止2024年02月19日，甲骨文云一共有如下[可用region](./resource/region.txt)，请结合
![REGION](./resource/region.png)
自行找到自己所对应的REGION，KEY或NAME都可以
2. COMPARTMENT

打开[https://cloud.oracle.com/identity/compartments](https://cloud.oracle.com/identity/compartments)，找到除开ManagedCompartmentForPaaS的另一个实际租户的ocid填入
![COMPARTMENT](./resource/compartment-id.png)
3. OCI_CONFIG_PRIVATE_PEM

打开[https://cloud.oracle.com/identity/domains/my-profile/api-keys](https://cloud.oracle.com/identity/domains/my-profile/api-keys)，创建一个API密钥
然后将保存的私钥文件的内容填入，并记录下指纹下步会使用
![fingerprint](./resource/fingerprint.png)
4. OCI_CONFIG_FILE

格式如下：
```
[DEFAULT]
user=$$
fingerprint=上一步的指纹
key_file=~/.oci/oci_api_key.pem
tenancy=第二步的COMPARTMENT
region=上面找到的那个region
```
打开[https://cloud.oracle.com/identity/domains/my-profile](https://cloud.oracle.com/identity/domains/my-profile)复制用户信息中的ocid替换$$