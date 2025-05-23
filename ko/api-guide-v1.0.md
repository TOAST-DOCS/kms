
## Security > Secure Key Manager > API v1.0 가이드

Secure Key Manager는 사용자 데이터에 접근할 수 있는 다양한 API를 제공합니다. 클라이언트는 키 저장소에 설정한 인증을 통과한 후 Secure Key Manager에 저장한 데이터를 사용할 수 있습니다.

## 기본 정보

### EndPoint
```text
https://api-keymanager.nhncloudservice.com
```

### API 목록

| Method | URI | 설명 |
|---|---|---|
| GET | /keymanager/v1.0/appkey/{appkey}/confirm | API를 호출한 클라이언트 정보를 제공합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/secrets/{keyid} | Secure Key Manager에 저장한 기밀 데이터를 조회합니다. |
| POST | /keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/encrypt | Secure Key Manager에 저장한 대칭 키로 데이터를 암호화합니다. |
| POST | /keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/decrypt | Secure Key Manager에 저장한 대칭 키로 데이터를 복호화합니다. |
| POST | /keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/create-local-key | 클라이언트가 로컬 환경에서 데이터 암/복호화에 사용할 수 있는 AES-256 대칭 키를 생성합니다. |
| GET | /keymanager/{v1.0\|v1.1}/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key | Secure Key Manager에 저장한 대칭 키를 조회합니다. |
| POST | /keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/sign | Secure Key Manager에 저장한 비대칭 키로 데이터를 서명합니다. |
| POST | /keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/verify | Secure Key Manager에 저장한 비대칭 키로 데이터와 서명을 검증합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/privateKey | Secure Key Manager에 저장한 개인 키를 조회합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/publicKey | Secure Key Manager에 저장한 공개 키를 조회합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores | Secure Key Manager에 저장된 키 저장소들을 조회합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId} | Secure Key Manager에 저장된 키 저장소를 상세 조회합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/keys | Secure Key Manager에 저장된 키 저장소의 키들을 조회합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/keys/{keyId} | Secure Key Manager에 저장된 키 저장소의 키를 상세 조회합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/ips | Secure Key Manager에 저장된 키 저장소의 IPv4 인증 정보들을 조회합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/ips?value={ipv4Value} | Secure Key Manager에 저장된 키 저장소의 IPv4 인증 정보를 상세 조회합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/macs | Secure Key Manager에 저장된 키 저장소의 MAC 인증 정보들을 조회합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/macs?value={macValue} | Secure Key Manager에 저장된 키 저장소의 MAC 인증 정보를 상세 조회합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/certificates | Secure Key Manager에 저장된 키 저장소의 인증서 인증 정보들을 조회합니다. |
| GET | /keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/certificates?value={certificateName} | Secure Key Manager에 저장된 키 저장소의 인증서 인증 정보를 상세 조회합니다. |

[API 요청의 HTTP 헤더]

Secure Key Manager의 MAC 주소 인증을 사용하려면 HTTP 헤더에 클라이언트 MAC 주소를 설정해서 요청해야 합니다.
```
X-TOAST-CLIENT-MAC-ADDR: {MAC 주소}
```

[API 요청의 경로 변수]

| 이름 | 타입 | 설명 |
|---|---|---|
| appkey | String | 사용하려는 데이터를 저장하고 있는 NHN Cloud 프로젝트의 앱키 |
| keyid | String | 사용하려는 데이터의 식별자 |

[API 응답의 데이터 공통 헤더]
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
| 이름 | 타입 | 설명 |
|---|---|---|
| resultCode | Number | API 호출 결과 코드값 |
| resultMessage | String | API 호출 결과 메시지 |
| isSuccessful | Boolean | API 호출 성공 여부 |

## 클라이언트 정보 조회
API를 호출한 클라이언트 정보를 조회할 때 사용합니다.
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
| 이름 | 타입 | 설명 |
|---|---|---|
| clientIp | String | API를 호출한 클라이언트의 IP 주소 |
| clientMacHeader | String |API를 호출한 클라이언트의 MAC 주소 헤더값 |
| clientSentCertificate | Boolean | API를 호출한 클라이언트가 인증서를 사용하고 있는지 여부 |

## 기밀 데이터

### 기밀 데이터 조회
Secure Key Manager에 저장한 기밀 데이터를 조회할 때 사용합니다.
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
| 이름 | 타입 | 설명 |
|---|---|---|
| secret | String | 기밀 데이터 조회 결과 |

## 대칭 키

### 대칭 키 암호화
Secure Key Manager에 생성한 대칭 키로 데이터를 암호화할 때 사용합니다. 사용자는 32KB 이하의 텍스트 데이터를 전달해서 Secure Key Manager에 저장한 대칭 키로 암호화할 수 있습니다.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/encrypt
```

[Request Body]

```
{
    "plaintext": "data"
}
```
| 이름 | 타입 | 설명 |
|---|---|---|
| plaintext | String | 대칭 키로 암호화할 데이터 |

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
| 이름 | 타입 | 설명 |
|---|---|---|
| ciphertext | String | 대칭 키로 데이터를 암호화한 결과 |
| keyVersion | Number | API 요청 처리에 사용한 대칭 키 버전 |

### 대칭 키 복호화
Secure Key Manager에 생성한 대칭 키로 데이터를 복호화할 때 사용합니다. 사용자는 암호화된 텍스트를 전달해서 Secure Key Manager에 저장한 대칭 키로 복호화할 수 있습니다.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/symmetric-keys/{keyid}/decrypt
```

[Request Body]
```
{
    "ciphertext": "AAAAABzGwQniNneKXmcOLhWnxEqC1rNY+UdVb3lyeX/4wSrP"
}
```
| 이름 | 타입 | 설명 |
|---|---|---|
| ciphertext | String | 대칭 키로 복호화할 데이터 |

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
| 이름 | 타입 | 설명 |
|---|---|---|
| plaintext | String | 대칭 키로 데이터를 복호화한 결과 |
| keyVersion | Number | API 요청 처리에 사용한 대칭 키 버전 |

### 대칭 키로 암호화한 로컬 대칭 키 생성
클라이언트가 로컬 환경에서 사용할 수 있는 AES-256 대칭 키를 생성할 때 사용합니다. localKeyPlaintext는 생성한 대칭 키를 Base64 인코딩한 형태이며 Base64 디코딩 후 바로 사용할 수 있습니다. localKeyCiphertext는 생성한 대칭 키를 Secure Key Manager에 저장한 대칭 키로 암호화한 후 Base64 인코딩한 형태이며 스토리지에 저장할 때 사용합니다. 스토리지에 저장한 대칭 키는 복호화 API를 사용해서 복호화한 후 사용할 수 있습니다.
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
| 이름 | 타입 | 설명 |
|---|---|---|
| localKeyPlaintext | String | Base64 인코딩한 AES-256 대칭 키 |
| localKeyCiphertext | String | Secure Key Manager에 저장한 대칭 키로 암호화한 후 Base64 인코딩한 AES-256 대칭 키 |
| keyVersion | Number | API 요청 처리에 사용한 대칭 키 버전 |

### 대칭 키 조회

Secure Key Manager에 저장한 대칭 키(AES-256)를 조회할 수 있습니다.

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
| 이름 | 타입 | 설명 |
|---|---|---|
| symmetricKey | String | 대칭 키 데이터(16진수 문자열 형태) |

#### v1.1
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.1/appkey/{appkey}/symmetric-keys/{keyid}/symmetric-key?keyVersion={keyVersion}
```

[Request Parameter]

| 이름 | 타입 | 설명 |
|---|---|---|
| keyVersion | Number | 조회하려는 대칭 키 버전 |

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
| 이름 | 타입 | 설명 |
|---|---|---|
| symmetricKey | String | 대칭 키 데이터(16진수 문자열 형태) |
| keyVersion | Number | API 요청 처리에 사용한 대칭 키 버전 |

## 비대칭 키

### 비대칭 키로 서명
Secure Key Manager에 생성한 비대칭 키로 데이터를 서명할 때 사용합니다. 사용자는 245 Byte 이하의 텍스트 데이터를 전달해서 Secure Key Manager에 저장한 비대칭 키로 서명할 수 있습니다.
```text
POST https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/sign
```

[Request Body]
```
{
    "plaintext": "data"
}
```
| 이름 | 타입 | 설명 |
|---|---|---|
| plaintext | String | 비대칭 키로 서명할 데이터 |

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
| 이름 | 타입 | 설명 |
|---|---|---|
| signature | String | 비대칭 키로 데이터를 서명한 서명값 |
| keyVersion | Number | API 요청 처리에 사용한 비대칭 키 버전 |

### 비대칭 키로 데이터 검증
Secure Key Manager에 생성한 비대칭 키로 데이터를 검증할 때 사용합니다. 사용자는 데이터와 서명값을 전달해서 Secure Key Manager에 저장한 비대칭 키로 데이터가 위변조되지 않았음을 검증할 수 있습니다.
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
| 이름 | 타입 | 설명 |
|---|---|---|
| plaintext | String | 비대칭 키로 검증할 데이터 |
| signature | String | 비대칭 키로 데이터를 서명한 서명값 |

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
| 이름 | 타입 | 설명 |
|---|---|---|
| result | Boolean | 비대칭 키로 데이터와 서명값을 검증한 결과 |
| keyVersion | Number | API 요청 처리에 사용한 비대칭 키 버전 |

### 개인 키 조회

Secure Key Manager에 저장한 비대칭 키 중 개인 키를 조회할 수 있습니다.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/privateKey?keyVersion={keyVersion}
```

[Request Parameter]

| 이름 | 타입 | 설명 |
|---|---|---|
| keyVersion | Number | 조회하려는 비대칭 키 버전 |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "keyType": "PrivateKey",
        "key": "0x30, 0x82, 0x04, 0xbe, 0x02, 0x01, 0x00, 0x30, 0x0d, 0x06, 0x09, 0x2a, 0x86, 0x48, 0x86, 0xf7, 0x0d, 0x01, 0x01, 0x01, 0x05, 0x00, 0x04, 0x82, 0x04, 0xa8, 0x30, 0x82, 0x04, 0xa4, 0x02, 0x01, 0x00, 0x02, 0x82, 0x01, 0x01, 0x00, 0x8b, 0x07, 0x8e, 0xda, 0xc7, 0x83, 0x95, 0xc8, 0x43, 0xa7, 0xb8, 0x31, 0x6f, 0xf6, 0x25, 0x36, 0x89, 0x64, 0xc5, 0x38, 0x75, 0x4b, 0xa6, 0x80, 0xfe, 0x7c, 0xc5, 0x6a, 0x94, 0xf2,
                ... 후략 ...",
        "encodedKey": "MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCLB47ax4OVyEOnuDFv9iU2iWTFOHVLpoD+fMVqlPJiiuJSwi5x/zd3LojWuUyr+dZ9Icxl23Alu4GwwKgUi4DL8qo8jD14THJoeUgIZ56wmYMvN+CkNnmkyqcGn6yT+AXtBJVGqS/2lssHLIGELi8XXkWdf6OBfig6HgsJAnix8Z+T/QdikEFUI5ZiuUWyHw2Bag9B4CoPF2EgXfu5HcW4GA4KH2PI92O4vNg8AmFVDk2E+ma2quSau7LjS3KY9s3Sq+JqvTPZmqHQJudv9ZYcnbyDG/
                       ... 후략 ...",
        "keyVersion": 0
    }
}
```
| 이름 | 타입 | 설명 |
|---|---|---|
| keyType | String | 비대칭 키 형태 |
| key | String | 개인 키 데이터(16진수 문자열 형태) |
| encodedKey | String | 개인 키 데이터(Base64 인코딩 형태) |
| keyVersion | Number | API 요청 처리에 사용한 비대칭 키 버전 |

### 공개 키 조회

Secure Key Manager에 저장한 비대칭 키 중 공개 키를 조회할 수 있습니다.
인증에 상관없이 조회할 수 있습니다.

```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/asymmetric-keys/{keyid}/publicKey?keyVersion={keyVersion}
```

[Request Parameter]

| 이름 | 타입 | 설명 |
|---|---|---|
| keyVersion | Number | 조회하려는 비대칭 키 버전 |

[Response Body]
```
{
    "header": {
        ...
    },
    "body": {
        "keyType": "PublicKey",
        "key": "0x30, 0x82, 0x01, 0x22, 0x30, 0x0d, 0x06, 0x09, 0x2a, 0x86, 0x48, 0x86, 0xf7, 0x0d, 0x01, 0x01, 0x01, 0x05, 0x00, 0x03, 0x82, 0x01, 0x0f, 0x00, 0x30, 0x82, 0x01, 0x0a, 0x02, 0x82, 0x01, 0x01, 0x00, 0x8b, 0x07, 0x8e, 0xda, 0xc7, 0x83, 0x95, 0xc8, 0x43, 0xa7, 0xb8, 0x31, 0x6f, 0xf6, 0x25, 0x36, 0x89, 0x64, 0xc5, 0x38, 0x75, 0x4b, 0xa6, 0x80, 0xfe, 0x7c, 0xc5, 0x6a, 0x94, 0xf2, 0x62, 0x8a, 0xe2, 0x52, 0xc2,
                ... 후략 ...",
        "encodedKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAiweO2seDlchDp7gxb/YlNolkxTh1S6aA/nzFapTyYoriUsIucf83dy6I1rlMq/nWfSHMZdtwJbuBsMCoFIuAy/KqPIw9eExyaHlICGeesJmDLzfgpDZ5pMqnBp+sk/gF7QSVRqkv9pbLByyBhC4vF15FnX+jgX4oOh4LCQJ4sfGfk/0HYpBBVCOWYrlFsh8NgWoPQeAqDxdhIF37uR3FuBgOCh9jyPdjuLzYPAJhVQ5NhPpmtqrkmruy40tymPbN0qviar0z2Zqh0Cbnb/WWHJ28gxv+d+iJCXJvm+fIg7hRYJ5C+mun/N6FB8QHv/
                       ... 후략 ...",
        "keyVersion": 0
    }
}
```
| 이름 | 타입 | 설명 |
|---|---|---|
| keyType | String | 비대칭 키 형태 |
| key | String | 공개 키 데이터(16진수 문자열 형태) |
| encodedKey | String | 공개 키 데이터(Base64 인코딩 형태) |
| keyVersion | Number | API 요청 처리에 사용한 비대칭 키 버전 |

## 키 저장소

### 키 저장소 목록 조회
Secure Key Manager에 생성한 키 저장소의 ID 목록을 조회할 수 있습니다.
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
| 이름 | 타입 | 설명 |
|---|---|---|
| keyStoreIdList | List | 키 저장소 ID 목록 |

### 키 저장소 상세 조회
Secure Key Manager에 생성한 키 저장소 정보를 상세 조회할 수 있습니다.
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
        "name": "키 저장소 이름",
        "description": "키 저장소 설명",
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
| 이름 | 타입 | 설명 |
|---|---|---|
| keyStoreId | Number | 키 저장소 ID |
| name | String | 키 저장소 이름 |
| description | String | 키 저장소 설명 |
| ip4AuthUse | String | 키 저장소 IPv4 인증 사용 여부(Y/N) |
| macAuthUse | String | 키 저장소 MAC 인증 사용 여부(Y/N) |
| certificateAuthUse | String | 키 저장소 인증서 인증 사용 여부(Y/N) |
| creationUser | String | 키 저장소 생성 유저 |
| creationDatetime | String | 키 저장소 생성 일시 |
| lastChangeUser | String | 키 저장소 마지막 수정 유저 |
| lastChangeDatetime | String | 키 저장소 마지막 수정 일시 |

## 키

### 키 목록 조회
Secure Key Manager에 생성한 키의 ID 목록을 조회할 수 있습니다.
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
| 이름 | 타입 | 설명 |
|---|---|---|
| keyIdList | List | 키 ID 목록 |

### 키 상세 조회
Secure Key Manager에 생성한 키 정보를 상세 조회할 수 있습니다.
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
        "name": "키 이름",
        "description": "키 설명",
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
| 이름 | 타입 | 설명 |
|---|---|---|
| keyId | Number | 키 ID |
| name | String | 키 이름 |
| description | String | 키 설명 |
| keyType | String | 키 타입(SECRET/SYMMETRIC_KEY/ASYMMETRIC_KEY) |
| currentKeyValueVersion | String | 현재 키 버전 |
| autoRotationPeriod | String | 키 회전 주기 |
| nextAutoRotationDate | String | 다음 키 회전일 |
| lastAccessDatetime | String | 키 마지막 사용 일시 |
| creationUser | String | 키 생성 유저 |
| creationDatetime | String | 키 생성 일시 |
| lastChangeUser | String | 키 마지막 수정 유저 |
| lastChangeDatetime | String | 키 마지막 수정 일시 |

## 인증 정보

### IPv4 인증 정보 목록 조회
Secure Key Manager에서 설정한 키 저장소의 IPv4 인증 정보 목록을 조회할 수 있습니다.
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
| 이름 | 타입 | 설명 |
|---|---|---|
| ipv4List | List | IPv4 인증 정보 목록 |

### IPv4 인증 정보 상세 조회
Secure Key Manager에서 설정한 키 저장소의 IPv4 인증 정보를 상세 조회할 수 있습니다.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/ips?value={ipv4Value}
```

[Request Parameter]

| 이름 | 타입 | 설명 |
|---|---|---|
| ipv4Value | String | 조회하려는 IPv4 주소 |

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
                "description": "IPv4 설명",
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
| 이름 | 타입 | 설명 |
|---|---|---|
| ipv4List | List | IPv4 인증 정보 목록 |
| value | String | IPv4 값 |
| description | String | IPv4 설명 |
| lastAccessDatetime | String | IPv4 마지막 사용 일시 |
| deletionDatetime | String | IPv4 삭제 예정 일시 |
| creationUser | String | IPv4 생성 유저 |
| creationDatetime | String | IPv4 생성 일시 |
| lastChangeUser | String | IPv4 마지막 수정 유저 |
| lastChangeDatetime | String | IPv4 마지막 수정 일시 |

### MAC 인증 정보 목록 조회
Secure Key Manager에서 설정한 키 저장소의 MAC 인증 정보 목록을 조회할 수 있습니다.
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
| 이름 | 타입 | 설명 |
|---|---|---|
| macList | List | MAC 인증 정보 목록 |

### MAC 인증 정보 상세 조회
Secure Key Manager에서 설정한 키 저장소의 MAC 인증 정보를 상세 조회할 수 있습니다.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/macs?value={macValue}
```

[Request Parameter]

| 이름 | 타입 | 설명 |
|---|---|---|
| macValue | String | 조회하려는 MAC 주소 |

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
                "description": "MAC 설명",
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
| 이름 | 타입 | 설명 |
|---|---|---|
| macList | List | MAC 인증 정보 목록 |
| value | String | MAC 값 |
| description | String | MAC 설명 |
| lastAccessDatetime | String | MAC 마지막 사용 일시 |
| deletionDatetime | String | MAC 삭제 예정 일시 |
| creationUser | String | MAC 생성 유저 |
| creationDatetime | String | MAC 생성 일시 |
| lastChangeUser | String | MAC 마지막 수정 유저 |
| lastChangeDatetime | String | MAC 마지막 수정 일시 |

### 인증서 인증 정보 목록 조회
Secure Key Manager에서 설정한 키 저장소의 인증서 인증 정보 목록을 조회할 수 있습니다.
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
| 이름 | 타입 | 설명 |
|---|---|---|
| certificateList | List | 인증서 인증 정보 목록 |

### 인증서 인증 정보 상세 조회
Secure Key Manager에서 설정한 키 저장소의 인증서 인증 정보를 상세 조회할 수 있습니다.
```text
GET https://api-keymanager.nhncloudservice.com/keymanager/v1.0/appkey/{appkey}/keystores/{keyStoreId}/certificates?value={certificateName}
```

[Request Parameter]

| 이름 | 타입 | 설명 |
|---|---|---|
| certificateName | String | 조회하려는 인증서 이름 |

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
                "description": "인증서 설명",
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
| 이름 | 타입 | 설명 |
|---|---|---|
| certificateList | List | 인증서 인증 정보 목록 |
| name | String | 인증서 이름 |
| password | String | 인증서 비밀번호 |
| description | String | 인증서 설명 |
| lastAccessDatetime | String | 인증서 마지막 사용 일시 |
| deletionDatetime | String | 인증서 삭제 예정 일시 |
| creationUser | String | 인증서 생성 유저 |
| creationDatetime | String | 인증서 생성 일시 |
| lastChangeUser | String | 인증서 마지막 수정 유저 |
| lastChangeDatetime | String | 인증서 마지막 수정 일시 |