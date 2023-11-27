## Security > Secure Key Manager > Console User Guide

Console User Guide describes basics for the use of Secure Key Manager:
- **Create a Key Store**
- **Create a Key**
- **Register Authentication Information**
- **Manage User Data**
- **Approval Feature**

### Create a Key Store
Secure Key Manager manages authentication information and keys in key store unit. If there is no key store, the following screen is displayed:

![console-guide-01](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-01.png)

Click **Add Key Store**, and a window to create a key store shows up.

![console-guide-02](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-02.png)

Enter name and description, select one or more authentication method, and then click **Add**, and a key store is created. The newly created key store shows up on the list of key stores like below:

![console-guide-03](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-03.png)

Click a key store from the list, and a menu to manage the key store is displayed as below:

![console-guide-04](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-04.png)

### Create a Key
In Secure Key Manager, keys are categorized into three types: Confidential Data, Symmetric Key, and Asymmetric Key. For Confidential Data, Secure Key Manager stores string data and provides query feature using APIs. For Symmetric key, data encryption/decryption using APIs is provided. For Asymmetric Key, data signing/verification using APIs is provided. Users can select a key type appropriate for purpose and create keys.

Click **Key Management**, and a page to manage keys shows up like below:

![console-guide-05](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-05.png)

On the key management page, click **Add Key** and a window to create a key is displayed. Depending on the selected key type, you may enter data as needed.

![console-guide-06](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-06.png)


![console-guide-07](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-07.png)


![console-guide-08](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-08.png)


If you select Confidential Data, you can enter name, description, and data. If you select Symmetric Key or Asymmetric Key, you can enter name, description, and rotation cycle. After entering required data, click **Add** and a key is created. Then, the created key is displayed on the key management page as below:

![console-guide-09](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-09.png)

### Import a Key
Secure Key Manager supports a feature to import a symmetric key (AES-256).

![console-guide-10](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-10.png)

You can upload a key by entering a key value in the **Key Data** area, and the format of key that can be uploaded is as follows.

```
0xXX, 0xXX, ..., 0xXX
```

Upload the key by entering 32 hexadecimal strings separated by comma (`,`) or space (` `) used as delimiters, as shown above.

### Register Authentication Information
Keys that are created in Secure Key Manager are available only for successfully authenticated clients. You may register authentication information for client authentication from the menu of **IPv4 Address Management**, **MAC Address Management**, and **Certificate Management**.

#### Register IPv4 Address
Click **IPv4 Address Management**, and a page to manage IPv4 address for client authentication shows up.

![console-guide-11](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-11.png)

Click **Add IPv4 Address**, and a window to add IPv4 address shows up as below:

![console-guide-12](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-12.png)

You can register not just IPv4 in the IP format and also IPv4 band using CIDR notation.

![console-guide-38](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2023-09-26-en/console-guide-38.png)

Enter client IPv4 address and description, and click **Add**, then the IPv4 address is added. Note that such IPv4 address must be same as the address that clients use to access Secure Key Manager. The newly added address is displayed on the IPv4 address management page.

![console-guide-13](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-13.png)

#### Register MAC Address
Click **MAC Address Management**, and the MAC address management page for client authentication shows up.
![console-guide-14](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-14.png)

Click **Add MAC Address**, and a window to add MAC address shows up.

![console-guide-15](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-15.png)

Enter Client MAC Address and description, and click **Add**, then the MAC address is added. The newly added MAC address shows up on the MAC address management page.

![console-guide-16](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-16.png)

#### Register Client Certificates
Click **Certificate Management**, and the certificate management page for client authentication shows up.

![console-guide-17](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-17.png)

Click **Add Certificates**, and a window to create a certificate shows up.

![console-guide-18](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-18.png)

Enter certificate name, password, and description, select usage period, and click **Add**, then a certificate is created. The newly created certificate shows up on the certificate management page like below. If you click the **Download** icon in the certificate management page, the certificate file is downloaded.

![console-guide-19](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-19.png)

### Manage User Data
Secure Key Manager provides detailed information on user-created data (e.g. key or authentication information). Click **Detail Key Information** on the list of user data, and details are displayed like below:

![console-guide-20](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-20.png)

#### Delete User Data

The initial status of user-created data is **In Service**. To delete unnecessary data, click **Request for Deletion** in the **Detail Key Information** window.

![console-guide-21](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-21.png)

Once requested for deletion, the data status is changed to **Scheduled to be Deleted**. Data in **Scheduled to be Deleted** status becomes unavailable and it is completely deleted in 7 days.

![console-guide-22](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-22.png)

You may click **Immediately Delete** for data in **Scheduled to be Deleted** status to delete the data without having to wait until the scheduled deletion time, or click **Cancel Deletion** to revert it to **In Service** status.

![console-guide-23](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-23.png)

#### Rotate Symmetric/Asymmetric Keys

In Secure Key Manager, symmetric/asymmetric keys can be rotated. Like shown below, auto rotation cycle can be set from the details page of Symmetric/Asymmetric Key. If you set the rotation cycle to '0', auto rotation is not enabled.

![console-guide-24](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-24.png)

If you set the rotation cycle to 30 or higher, the next rotation date is displayed, and key is automatically rotated at every rotation cycle.

![console-guide-25](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-25.png)

On the Detail Key Information page for Symmetric/Asymmetric Key, click **Immediately Rotate** to immediately rotate the key.

![console-guide-26](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-26.png)

When a key is rotated, a new version is added to the list of key versions, like below:

![console-guide-27](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-27.png)

As an exception, keys generated through key import do not provide the key rotation feature, unlike symmetric keys generated by Secure Key Manager. When you query the key, the key rotation area does not exist as shown below:

![console-guide-28](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-28.png)

### Approval Feature

#### Enable Approval Feature
Enable Approval Feature of Secure Key Manager in Approval Process Management Setting on Governance Setting under Organization Management.

![console-guide-29](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-29.png)

#### Set up Roles for Approval Feature
On Member Management in Secure Key Manager, perform the approval process by obtaining the approver role (APPROVAL ADMIN) and the requester role (APPROVAL MEMBER).

![console-guide-30](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-30.png)

#### Differences with Approval Feature enabled
When you obtain the approver or requester role after enabling the approval feature, the **Approval List** and **Key Store Management** tabs are added to Secure Key Manager. Only the approver and requester can access these tabs.

![console-guide-31](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-31.png)

When you enable the approval feature, data can no longer be added, modified, or deleted in the key store. When requesting for change, move to the **Key Store Management** tab.

![console-guide-32](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-32.png)

#### Make Approval Requests
On the **Key Store Management** tab, the approver and requester make a request for approval of changes for each key store. Addition, modification, and deletion are performed through a similar operation to the existing keystore. Changes to keys and authentication information are displayed in Status as follows.

![console-guide-33](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-33.png)

![console-guide-34](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-34.png)

Make a request for approval with the **Request Approval** button in the key store, and the requests made for a project can be found in the **Approval List** tab.

![console-guide-35](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-35.png)

#### Apply Approval Requests
On the  **Approval List** tab, the approver confirms the requst for approval of changes and determines whether to apply the request by selecting **Approve** or **Deny**.

![console-guide-36](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-36.png)

The request is applied immediately upon clicking Approve. The change can be found in the **Key Depository** or the **Key Store Management** tab.

![console-guide-37](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-37.png)

### Authorization for Add/Delete Keys API

#### Create User Access Key ID, Secret Access Key

Click the ID area in the upper-right corner of the console to see the **API Security Settings** menu as follows.

![console-guide-38](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2023-11-28-en/console-guide-01.png)

In **API Security Setting**, you can click **Create User Access Key ID**to create a **User Access Key ID** and **Secret Access Key**that must be entered into the Secure Key Manager Add/Delete Keys API.

![console-guide-39](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2023-11-28-en/console-guide-02.png)

![console-guide-40](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2023-11-28-en/console-guide-03.png)

After creating **User Access Key ID** and **Secret Access Key**, the **Completed to Issue Secret Key** screen is displayed as shown below. The secret key is only given to you once in that popup screen, so make sure to keep a good record of this value.

![console-guide-41](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2023-11-28-en/console-guide-04.png)

The **User Access Key ID**, which is required for API requests, can be found by closing the secret key successfully issued popup.

![console-guide-42](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2023-11-28-en/console-guide-05.png)