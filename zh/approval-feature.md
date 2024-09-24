## Security > Secure Key Manager > Console User Guide > Approval Feature

This document describes the approval features of Secure Key Manager that you use to meet the requirements for secure encryption key management as required by national and international security certification audits (ISMS-P, ISO, etc.).

The document explores how to **Enable Approval Feature**, setting up approval-related roles, the differences between before and after, and the **Approval Process** after enabling the feature.

![approval-feature](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2024-02-27-en/approval-feature.png)

## Enable Approval Feature

### How to Enable Approval Feature
Enable Approval Feature of Secure Key Manager in Approval Process Management Setting on Governance Setting under Organization Management.

![console-guide-29](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-29.png)

### Set up Roles for Approval Feature
On Member Management in Secure Key Manager, perform the approval process by obtaining the approver role (APPROVAL ADMIN) and the requester role (APPROVAL MEMBER).

![console-guide-30](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-30.png)

### Differences with Approval Feature enabled
When you obtain the approver or requester role after enabling the approval feature, the **Approval List** and **Key Store Management** tabs are added to Secure Key Manager. Only the approver and requester can access these tabs.

![console-guide-31](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-31.png)

When you enable the approval feature, data can no longer be added, modified, or deleted in the key store. When requesting for change, move to the **Key Store Management** tab.

![console-guide-32](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-32.png)

## Approval Process

### Make Approval Requests
On the **Key Store Management** tab, the approver and requester make a request for approval of changes for each key store. Addition, modification, and deletion are performed through a similar operation to the existing keystore. Changes to keys and authentication information are displayed in Status as follows.

![console-guide-33](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-33.png)

![console-guide-34](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-34.png)

Make a request for approval with the **Request Approval** button in the key store, and the requests made for a project can be found in the **Approval List** tab.

![console-guide-35](http://static.toastoven.net/prod_kms/2024-09-25-en/console-guide-35.png)

### Apply Approval Requests
On the  **Approval List** tab, the approver confirms the requst for approval of changes and determines whether to apply the request by selecting **Approve** or **Deny**.

![console-guide-36](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-36.png)

The request is applied immediately upon clicking Approve. The change can be found in the **Key Depository** or the **Key Store Management** tab.

![console-guide-37](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-37.png)
