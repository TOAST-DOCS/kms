
## Security > Secure Key Manager > API v1.0 Guide

Secure Key Manager provides various APIs to access user data. Clients must be authenticated via key store to get access to data stored in Secure Kay Manager.

## Basic Information

### EndPoint
```text
https://api-keymanager.nhncloudservice.com
```

### List of APIs

| Method | URI | Description |
|---|---|---|
| GET | /keymanager/v1.0/appkey/{appkey}/confirm | Provide information of the client that called API. |
| GET | /keymanager/v1.0/appkey/{appkey}/secrets/{keyid} | Query confidential data stored in Secure Key Manager. |
| POST | /keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/encrypt | Encrypt data with the symmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/decrypt | Decrypt data with the symmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/create-local-key | Create AES-256 symmetric keys that can be used by a client for data encryption/decryption in local environment. |
| GET | /keymanager/{v1.0\|v1.1}/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key | Query the symmetric key stored in Secure Key Manager.|
| POST | /keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/sign | Sign data with the asymmetric key stored in Secure Key Manager. |
| POST | /keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/verify | Verify data and signature with the asymmetric key stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/privateKey | Query the private key stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/publicKey | Query the public key stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores | Query the key stores stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId} | Query the details of the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/keys | Query the keys in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/keys/{keyId} | Query the details of the key in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/ips | Query the IPv4 authentication information in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/ips?value={ipv4Value} | Query the details of the IPv4 authentication information in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/macs | Query the MAC authentication information in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/macs?value={macValue} | Query the details of the MAC authentication information in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/certificates | Query the certificate authentication information in the key store stored in Secure Key Manager. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/certificates?value={certificateName} | Query the details of the certificate authentication information in the key store stored in Secure Key Manager. |

[HTTP Header of API Request]

To use MAC address authentication of Secure Key Manager, you must make a request by setting the client's MAC address in the HTTP header.
```
X-TOAST-CLIENT-MAC-ADDR: {MAC Address}
```

[Path Variables of API Request]

| Name | Type | Description |
|---|---|---|
| appkey | String | Appkey of the NHN Cloud project where the data in need is stored |
| keyid | String | Identifier of data in need |

[Common Data Header of API Response]
```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "body": {
        ...
    }
}
```
| Name | Type | Description |
|---|---|---|
| resultCode | Number | Result code value of API call |
| resultMessage | String | Result message of API call |
| isSuccessful | Boolean | Whether API call is successful or not |

## Query Client Information
This API is used to query information of the client that called API.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/confirm
```
[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "clientIp": "0.0.0.0",
        "clientMacHeader": "00:00:00:00:00:00",
        "clientSentCerfificate": false
    }
}
```
| Name | Type | Description |
|---|---|---|
| clientIp | String | IP address of the client that called API |
| clientMacHeader | String |Header value of MAC address of the client that called API |
| clientSentCertificate | Boolean | Whether the client that called API is using certificate or not |

## Confidential Data

### Query Confidential Data
This API is used to query confidential data stored in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/secrets/{keyid}
```

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "secret": "data"
    }
}
```
| Name | Type | Description |
|---|---|---|
| secret | String | Query result of confidential data |

## Symmetric Key

### Encrypt Symmetric Keys
This API is used to encrypt data with the symmetric key created in Secure Key Manager. A user can pass 32KB or smaller text data, and the data can be encrypted with the symmetric key stored in Secure Key Manager.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/encrypt
```

[Request Body]

```
{
    "plaintext": "data"
}
```
| Name | Type | Description |
|---|---|---|
| plaintext | String | Data to be encrypted with the symmetric key |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "ciphertext": "AAAAABzGwQniNneKXmcOLhWnxEqC1rNY+UdVb3lyeX/4wSrP",
        "keyVersion": 1
    }
}
```
| Name | Type | Description |
|---|---|---|
| ciphertext | String | Result of data encryption with the symmetric key |
| keyVersion | Number | Version of the symmetric key used for processing the API request |

### Decrypt Symmetric Keys
This API is used to decrypt data with the symmetric key created in Secure Key Manager. A use can pass encrypted text, and the text data can be decrypted with the symmetric key stored in Secure Key Manager.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/decrypt
```

[Request Body]
```
{
    "ciphertext": "AAAAABzGwQniNneKXmcOLhWnxEqC1rNY+UdVb3lyeX/4wSrP"
}
```
| Name | Type | Description |
|---|---|---|
| ciphertext | String | Data to be decrypted with the symmetric key |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "plaintext": "data",
        "keyVersion": 1
    }
}
```
| Name | Type | Description |
|---|---|---|
| plaintext | String | Result of data decryption with the symmetric key |
| keyVersion | Number | Version of the symmetric key used for processing the API request |

### Generate Local Symmetric Keys Encrypted with the Symmetric Key
This API is used to create AES-256 symmetric keys that a client can use in local environment. localKeyPlaintext is a base64-encoded form of the generated symmetric key, and it is readily available after base64 decoding. localKeyCiphertext is a base64-encoded form of the generated symmetric key encrypted with the symmetric key stored in Secure Key Manager, and it is used to store data in a storage. The symmetric key stored in storage can be used after being decrypted by using the decryption API.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/create-local-key
```

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "localKeyPlaintext": "srV7MWkYIfYBknkASzwSEK1Z1y9Nx0f/RMZ3MSVIjm8=",
        "localKeyCiphertext": "v1s1WkiIj3KR+AafnupNv9xcX/JhL4GUzUr8mzLRpjbGuoAwU/GgboM/6QdRRY24",
        "keyVersion": 1
    }
}
```
| Name | Type | Description |
|---|---|---|
| localKeyPlaintext | String | Base64-encoded AES-256 symmetric key |
| localKeyCiphertext | String | Base64-encoded AES-256 symmetric key encrypted with the symmetric key stored in Secure Key Manager |
| keyVersion | Number | Version of the symmetric key used for processing the API request |

### Query the Symmetric Key

Users can query the symmetric key (AES-256) stored in Secure Key Manager.

#### v1.0
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key
```

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "symmetricKey": "0x00, 0x20, 0x00, 0x41, 0x00, 0x20, 0x00, 0x73, 0x00, 0x69, 0x00, 0x6d, 0x00, 0x70, 0x00, 0x6c, 0x00, 0x65, 0x00, 0x20, 0x00, 0x4a, 0x00, 0x61, 0x00, 0x76, 0x00, 0x61, 0x00, 0x2e, 0x00, 0x20"
    }
}
```
| Name | Type | Description |
|---|---|---|
| symmetricKey | String | Symmetric key data (Hex string form) |

#### v1.1
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.1/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key?keyVersion={keyVersion}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| keyVersion | Number | Version of the symmetric key to query |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "symmetricKey": "0x00, 0x20, 0x00, 0x41, 0x00, 0x20, 0x00, 0x73, 0x00, 0x69, 0x00, 0x6d, 0x00, 0x70, 0x00, 0x6c, 0x00, 0x65, 0x00, 0x20, 0x00, 0x4a, 0x00, 0x61, 0x00, 0x76, 0x00, 0x61, 0x00, 0x2e, 0x00, 0x20",
        "keyVersion": 1
    }
}
```
| Name | Type | Description |
|---|---|---|
| symmetricKey | String | Symmetric key data (Hex string form) |
| keyVersion | Number |  Version of the symmetric key used for processing the API request |

## Asymmetric Key

### Sign with the Asymmetric Key
This API is used to sign data with the asymmetric key created in Secure Key Manager. Users can pass 245 Byte or smaller text data, and the data is signed with the asymmetric key stored in Secure Key Manager.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/sign
```

[Request Body]
```
{
    "plaintext": "data"
}
```
| Name | Type | Description |
|---|---|---|
| plaintext | String | Data to sign with the asymmetric key |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "signature": "AAAAAGI9zf831DX...",
        "keyVersion": 1
    }
}
```
| Name | Type | Description |
|---|---|---|
| signature | String | Signature value of signing the data with the asymmetric key |
| keyVersion | Number | Version of the asymmetric key used for processing the API request |

### Verify Data with the Asymmetric Key
This API is used to verify data with the asymmetric key created in Secure Key Manager. Users can pass data and signature value, and use asymmetric keys stored in Secure Key Manager to verify that data has not been forged.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/verify
```

[Request Body]

```
{
    "plaintext": "data",
    "signature": "AAAAAGI9zf831DX..."
}
```
| Name | Type | Description |
|---|---|---|
| plaintext | String | Data to be verified with the asymmetric key |
| signature | String | Signature value of signing the data with the asymmetric key |

[Response Body]

```
{
    "header": {
        ...
    },
    "body": {
        "result": true,
        "keyVersion": 1
    }
}
```
| Name | Type | Description |
|---|---|---|
| result | Boolean | Result of verifying data and signature value with the asymmetric key |
| keyVersion | Number | Version of the asymmetric key used for processing the API request |

### Query the Private Key

Users can query the private key among the asymmetric keys stored in Secure Key Manager.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/privateKey?keyVersion={keyVersion}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| keyVersion | Number | Version of the asymmetric key to query |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "keyType": "PrivateKey",
        "key": "0x30, 0x82, 0x04, 0xbe, 0x02, 0x01, 0x00, 0x30, 0x0d, 0x06, 0x09, 0x2a, 0x86, 0x48, 0x86, 0xf7, 0x0d, 0x01, 0x01, 0x01, 0x05, 0x00, 0x04, 0x82, 0x04, 0xa8, 0x30, 0x82, 0x04, 0xa4, 0x02, 0x01, 0x00, 0x02, 0x82, 0x01, 0x01, 0x00, 0x8b, 0x07, 0x8e, 0xda, 0xc7, 0x83, 0x95, 0xc8, 0x43, 0xa7, 0xb8, 0x31, 0x6f, 0xf6, 0x25, 0x36, 0x89, 0x64, 0xc5, 0x38, 0x75, 0x4b, 0xa6, 0x80, 0xfe, 0x7c, 0xc5, 0x6a, 0x94, 0xf2,
                ... ",
        "encodedKey": "MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCLB47ax4OVyEOnuDFv9iU2iWTFOHVLpoD+fMVqlPJiiuJSwi5x/zd3LojWuUyr+dZ9Icxl23Alu4GwwKgUi4DL8qo8jD14THJoeUgIZ56wmYMvN+CkNnmkyqcGn6yT+AXtBJVGqS/2lssHLIGELi8XXkWdf6OBfig6HgsJAnix8Z+T/QdikEFUI5ZiuUWyHw2Bag9B4CoPF2EgXfu5HcW4GA4KH2PI92O4vNg8AmFVDk2E+ma2quSau7LjS3KY9s3Sq+JqvTPZmqHQJudv9ZYcnbyDG/
                       ... ",
        "keyVersion": 0
    }
}
```
| Name | Type | Description |
|---|---|---|
| keyType | String | Asymmetric key form |
| key | String | Private key data (Hex string form) |
| encodedKey | String | Private key data (Base64-encoded form) |
| keyVersion | Number | Version of asymmetric key used for processing API requests |

### Query the Public Key

Users can query the public key among the asymmetric keys stored in Secure Key Manager, regardless of authentication.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/publicKey?keyVersion={keyVersion}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| keyVersion | Number | Version of asymmetric key to query |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "keyType": "PublicKey",
        "key": "0x30, 0x82, 0x01, 0x22, 0x30, 0x0d, 0x06, 0x09, 0x2a, 0x86, 0x48, 0x86, 0xf7, 0x0d, 0x01, 0x01, 0x01, 0x05, 0x00, 0x03, 0x82, 0x01, 0x0f, 0x00, 0x30, 0x82, 0x01, 0x0a, 0x02, 0x82, 0x01, 0x01, 0x00, 0x8b, 0x07, 0x8e, 0xda, 0xc7, 0x83, 0x95, 0xc8, 0x43, 0xa7, 0xb8, 0x31, 0x6f, 0xf6, 0x25, 0x36, 0x89, 0x64, 0xc5, 0x38, 0x75, 0x4b, 0xa6, 0x80, 0xfe, 0x7c, 0xc5, 0x6a, 0x94, 0xf2, 0x62, 0x8a, 0xe2, 0x52, 0xc2,
                ... ",
        "encodedKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAiweO2seDlchDp7gxb/YlNolkxTh1S6aA/nzFapTyYoriUsIucf83dy6I1rlMq/nWfSHMZdtwJbuBsMCoFIuAy/KqPIw9eExyaHlICGeesJmDLzfgpDZ5pMqnBp+sk/gF7QSVRqkv9pbLByyBhC4vF15FnX+jgX4oOh4LCQJ4sfGfk/0HYpBBVCOWYrlFsh8NgWoPQeAqDxdhIF37uR3FuBgOCh9jyPdjuLzYPAJhVQ5NhPpmtqrkmruy40tymPbN0qviar0z2Zqh0Cbnb/WWHJ28gxv+d+iJCXJvm+fIg7hRYJ5C+mun/N6FB8QHv/
                       ... ",
        "keyVersion": 0
    }
}
```
| Name | Type | Description |
|---|---|---|
| keyType | String | Asymmetric key form |
| key | String | Public key data (Hex string form) |
| encodedKey | String | Public key data (Base64-encoded form) |
| keyVersion | Number | Version of asymmetric key used for processing API requests |

## Key Store

### Query the List of Key stores
Users can query the list of IDs for key stores created in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "keyStoreIdList": [
            1,
            2,
            ...
        ]
    }
}
```
| Name | Type | Description |
|---|---|---|
| keyStoreIdList | List | List of key store IDs |

### Query the Details of the Key Store
Users can query detailed information about the key store created in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "keyStoreId": 1,
        "name": "Key store name",
        "description": "Key store description",
        "ip4AuthUse": "Y",
        "macAuthUse": "N",
        "certificateAuthUse": "Y",
        "creationUser": "SECURE_KEY_MANAGER",
        "creationDatetime": "2025-01-25T12:00:00",
        "lastChangeUser": "SECURE_KEY_MANAGER",
        "lastChangeDatetime": "2025-01-30T15:00:00.000"
    }
}
```
| Name | Type | Description |
|---|---|---|
| keyStoreId | Number | Key store ID |
| name | String | Key store name |
| description | String | Key store descriptions |
| ip4AuthUse | String | Whether IPv4 authentication is enabled for the key store or not (Y/N) |
| macAuthUse | String | Whether MAC authentication is enabled for the key store or not (Y/N) |
| certificateAuthUse | String | Whether the certificate authentication is enabled for the key store or not (Y/N) |
| creationUser | String | User who created the key store |
| creationDatetime | String | Key store creation date and time |
| lastChangeUser | String | Key store last modified user |
| lastChangeDatetime | String | Key store last modified date and time |

## Key

### Query the List of Keys
Users can query the list of key IDs created in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/keys
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "keyIdList": [
            "035a0ffa16a64bbf8171c4bdcea37bbf",
            "04fde6d8ee604cbe8fa7abe135a7dc3e",
            ...
        ]
    }
}
```
| Name | Type | Description |
|---|---|---|
| keyIdList | List | Key ID list |

### Query the details of keys
Users can query detailed information about the key created in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/keys/{keyId}
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "keyId": "035a0ffa16a64bbf8171c4bdcea37bbf",
        "name": "Key name",
        "description": "Key descriptions",
        "keyType": "SYMMETRIC_KEY",
        "currentKeyValueVersion": 2,
        "autoRotationPeriod": 0,
        "nextAutoRotationDate": null,
        "lastAccessDatetime": "2021-12-13T15:13:13.377",
        "deletionDatetime": null,
        "creationUser": "SECURE_KEY_MANAGER",
        "creationDatetime": "2025-01-25T12:00:00",
        "lastChangeUser": "SECURE_KEY_MANAGER",
        "lastChangeDatetime": "2025-01-30T15:00:00.000"
    }
}
```
| Name | Type | Description |
|---|---|---|
| keyId | Number | Key ID |
| name | String | Key name |
| description | String | Key descriptions |
| keyType | String | Key type(SECRET/SYMMETRIC_KEY/ASYMMETRIC_KEY) |
| currentKeyValueVersion | String | Current key version |
| autoRotationPeriod | String | Key rotation cycle |
| nextAutoRotationDate | String | Key next rotation date |
| lastAccessDatetime | String | Key last used date and time |
| creationUser | String | User who created the key |
| creationDatetime | String | Key creation date and time |
| lastChangeUser | String | Key last modified user |
| lastChangeDatetime | String | Key last modified date and time |

## Authentication Information

### Query the List of IPv4 Authentication Information
Users can query the list of IPv4 authentication information in the key store configured in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/ips
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "ipv4List": [
            "127.0.0.1",
            "127.0.0.2",
            ...
        ]
    }
}
```
| Name | Type | Description |
|---|---|---|
| ipv4List | List | IPv4 authentication information list |

### Query the details of IPv4 Authentication Information
Users can query detailed information about the IPv4 authentication in the key store configured in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/ips?value={ipv4Value}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| ipv4Value | String | IPv4 address to query |

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "ipv4List": [
            {
                "value": "127.0.0.1",
                "description": "IPv4 descriptions",
                "lastAccessDatetime": "2025-01-25T13:00:00",
                "deletionDatetime": null,
                "creationUser": "SECURE_KEY_MANAGER",
                "creationDatetime": "2025-01-25T12:00:00",
                "lastChangeUser": "SECURE_KEY_MANAGER",
                "lastChangeDatetime": "2025-01-30T15:00:00.000"
            }
        ]
    }
}
```
| Name | Type | Description |
|---|---|---|
| ipv4List | List | IPv4 authentication information list |
| value | String | IPv4 value |
| description | String | IPv4 descriptions |
| lastAccessDatetime | String | IPv4 last used date and time |
| deletionDatetime | String | IPv4 deletion scheduled date and time |
| creationUser | String | User who created the IPv4 |
| creationDatetime | String | IPv4 creation date and time |
| lastChangeUser | String | IPv4 last modified user |
| lastChangeDatetime | String | IPv4 last modified date and time |

### Query the List of MAC Authentication Information
Users can query the list of MAC authentication information in the key store configured in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/macs
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "macList": [
            "aa:aa:aa:aa:aa:aa",
            "bb:bb:bb:bb:bb:bb",
            ...
        ]
    }
}
```
| Name | Type | Description |
|---|---|---|
| macList | List | MAC authentication information list |

### Query the details of MAC Authentication Information
Users can query detailed information about the MAC authentication in the key store configured in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/macs?value={macValue}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| macValue | String | MAC address to query |

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "macList": [
            {
                "value": "aa:aa:aa:aa:aa:aa",
                "description": "MAC descriptions",
                "lastAccessDatetime": "2025-01-25T13:00:00",
                "deletionDatetime": null,
                "creationUser": "SECURE_KEY_MANAGER",
                "creationDatetime": "2025-01-25T12:00:00",
                "lastChangeUser": "SECURE_KEY_MANAGER",
                "lastChangeDatetime": "2025-01-30T15:00:00.000"
            }
        ]
    }
}
```
| Name | Type | Description |
|---|---|---|
| macList | List | MAC authentication information list |
| value | String | MAC value |
| description | String | MAC descriptions |
| lastAccessDatetime | String | MAC last used date and time |
| deletionDatetime | String | MAC deletion scheduled date and time |
| creationUser | String | User who created the MAC |
| creationDatetime | String | MAC creation date and time |
| lastChangeUser | String | MAC last modified user |
| lastChangeDatetime | String | MAC last modified date and time |

### Query the List of Certificate Authentication Information
Users can query the list of the certifacate authentication information in the key store configured in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/certificates
```

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "certificateList": [
            "certificate1",
            "certtificate2",
            ...
        ]
    }
}
```
| Name | Type | Description |
|---|---|---|
| certificateList | List | Certifacate authentication information list |

### Query the details of Certifacate Authentication Information
Users can query detailed information about the certifacate authentication in the key store configured in Secure Key Manager.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/certificates?value={certificateName}
```

[Request Parameter]

| Name | Type | Description |
|---|---|---|
| certificateName | String | Certificate name to query |

[Response Body]
```
{
    "header": {
        ...
    },
     "body": {
        "certificateList": [
            {
                "name": "certificate1",
                "password": "password1",
                "description": "Certificate descriptions",
                "expirationDate": "2029-07-21T10:26:47",
                "lastAccessDatetime": "2025-01-25T13:00:00",
                "deletionDatetime": null,
                "creationUser": "SECURE_KEY_MANAGER",
                "creationDatetime": "2025-01-25T12:00:00",
                "lastChangeUser": "SECURE_KEY_MANAGER",
                "lastChangeDatetime": "2025-01-30T15:00:00.000"
            }
        ]
    }
}
```
| Name | Type | Description |
|---|---|---|
| certificateList | List | Certificate authentication information list |
| name | String | Certificate name |
| password | String | Certificate password |
| description | String | Certificate descriptions |
| lastAccessDatetime | String | Certificate last used date and time |
| deletionDatetime | String | Certificate deletion scheduled date and time |
| creationUser | String | User who created the certificate |
| creationDatetime | String | Certificate creation date and time |
| lastChangeUser | String | Certificate last modified user |
| lastChangeDatetime | String | Certificate last modified date and time |
