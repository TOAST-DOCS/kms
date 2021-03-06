## Security > Secure Key Manager > 控制台使用指南

控制台使用指南介绍使用Secure Key Manager所需的基本内容。
- **创建密钥库**
- **创建密钥**
- **登录验证信息**
- **管理用户数据**

### 创建密钥库
Secure Key Manager以密钥库为单位管理验证信息和密钥。如果没有密钥库，则显示如下界面。

![console-guide-01](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-01.png)

单击**添加密钥库**，显示可创建密钥库的窗口。

![console-guide-02](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-02.png)

输入名称和说明并选择一个以上验证方法后单击**添加**按钮，创建密钥库。创建的密钥库如下图显示在密钥库列表中。

![console-guide-03](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-03.png)

在密钥库列表中单击密钥库，如下图显示可以管理密钥库的菜单。

![console-guide-04](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-04.png)

### 创建密钥
Secure Key Manager将密钥分为3种类型。机密数据保存字符串数据并提供使用API的查询功能。对称密钥提供使用API的数据加/解密功能。非对称密钥提供使用API的数据签名/验证功能。用户可选择符合使用目的的密钥类型后创建密钥。

单击**管理密钥**菜单，如下图显示可以管理密钥的界面。

![console-guide-05](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-05.png)

在管理密钥界面单击**添加密钥**，显示可创建密钥的窗口。根据选择的密钥类型，可输入所需数据。

![console-guide-06](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-06.png)


![console-guide-07](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-07.png)


![console-guide-08](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-08.png)


若选择机密数据，可输入名称、说明、数据，若选择对称密钥/非对称密钥时，可输入名称、说明、旋转周期。输入必需数据后单击**添加**，创建密钥。创建的密钥如下图显示在管理密钥界面。

![console-guide-09](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-09.png)

### 登录验证信息
Secure Key Manager中创建的密钥仅限验证成功的客户可使用。客户验证使用的验证信息登录在**管理IPv4地址**、**管理MAC地址**、***管理证书**菜单中。

#### 登录IPv4地址
单击**管理IPv4地址**，则如下图显示客户验证中使用的管理IPv4地址界面。

![console-guide-10](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-10.png)

单击**添加IPv4地址**，则如图所显示可添加IPv4地址的窗口。

![console-guide-11](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-11.png)

输入客户IPv4地址与说明后单击**添加**，添加IPv4地址。此时IPv4地址应输入客户访问Secure Key Manager时使用的IPv4地址。添加的IPv4地址如下图显示在管理IPv4地址界面中。

![console-guide-12](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-12.png)

#### 登录MAC地址
单击**管理MAC地址**，显示可客户验证中使用的管理MAC地址界面。
![console-guide-13](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-13.png)

单击**添加MAC地址**，显示可添加MAC地址的窗口。

![console-guide-14](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-14.png)

输入客户MAC地址与说明后单击**添加**，添加MAC地址。添加的MAC地址显示在管理MAC地址界面。

![console-guide-15](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-15.png)

#### 登录客户认证书
单击**管理认证书**，显示客户验证中使用的管理认证书界面。

![console-guide-16](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-16.png)

单击**添加认证书**，显示可以创建认证书的窗口。

![console-guide-17](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-17.png)

输入认证书名、密码、说明并选择使用期间后单击**添加**按钮，创建认证书。创建的认证书如下显示在管理认证书界面。在管理认证书界面单击**下载**图标，则下载认证书文件。

![console-guide-18](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-18.png)

### 管理用户数据
Secure Key Manager提供用户创建的数据（密钥、验证信息）的详细信息。在用户数据列表中单击**详细信息图标**时，如下图显示详细信息。

![console-guide-19](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-19.png)

#### 删除用户数据

用户创建的数据的初始状态为**正在使用**。若欲删除不需要的数据，如下图所示在**详细信息**窗口中单击**请求删除**。

![console-guide-20](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-20.png)

若请求删除，则如下图所示数据状态更改为**即将删除**。更改为**即将删除**的数据无法使用，7天后彻底删除。

![console-guide-21](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-21.png)

**即将删除**状态的数据，可单击**立即删除**，不等待至预定删除时间，直接删除，或可以单击**取消删除**，返回**正在使用**状态。

![console-guide-22](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-22.png)

#### 旋转对称密钥/非对称密钥

可在Secure Key Manager中旋转对称密钥/非对称密钥。如下图所示，在对称密钥/非对称密钥详细信息窗口中可设置自动旋转周期。若将旋转周期设置为0，则不使用自动旋转。

![console-guide-23](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-23.png)

如果在旋转周期中设置30以上的值，则显示下一旋转日，每个旋转周期自动旋转密钥。

![console-guide-24](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-24.png)

在对称密钥/非对称密钥的详细信息窗口中单击**立即旋转**，则可立即旋转密钥。

![console-guide-25](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-25.png)

若旋转密钥，则如下图所示，在密钥版本列表中添加新版本。

![console-guide-26](http://static.toastoven.net/prod_kms/2020-03-24/console-guide-26.png)
