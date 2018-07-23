## Accesskey管理

****

为了保证云资源的使用安全，当以API调用相关资源和操作时，要求使用Access Key验证您和应用程序的身份，以确保访问者具有相关权限。Access Key包含它由Access Key ID和Access Key Secret构成。拥有您的Access Key的任何人将与您拥有相同的资源访问和操作权限，可以无限制的访问您账户中的所有资源并进行相应的操作。您可以创建、禁用或删除您的Access Key，同时也建议您定期轮换Access Key以保证您的账户和资源安全。

每个主账号可拥有5组有效访问密钥，每个IAM用户可拥有2组有效的访问密钥，这在您必须轮换用户的访问密钥时非常有用。您可以禁用用户的访问密钥，这意味着该密钥不能用于 API 调用，在轮换密钥或取消用户对 API 的访问时，可以执行此操作。您可以随时删除访问密钥，不过，当您删除访问密钥时，意味着永久删除且无法恢复。

### 主账户的Accesskey管理

![主账号AK1.png](https://img1.jcloudcs.com/cms/9f6c8d72-721b-4d99-8d86-633d7df587d320180621203620.png)

###

### 主账号为子账号管理Accesskey

![子账号AK1.png](https://img1.jcloudcs.com/cms/d0ef03b6-4ffc-4696-a47f-3e7f7687c3b520180621203809.png)

###

### 子账号的Accesskey管理

![子账号   AK2.png](https://img1.jcloudcs.com/cms/08efd3fc-a1eb-4d0c-abbc-5d9ff64ca69620180621203650.png)