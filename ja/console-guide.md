## Security > Secure Key Manager > コンソール使用ガイド

コンソール使用ガイドではSecure Key Managerを使用するのに必要な基本的な内容を説明します。
- **キー保存場所の作成**
- **キーの作成**
- **認証情報の登録**
- **ユーザーデータの管理**
- **承認機能**

### キー保存場所の作成
Secure Key Managerは、キー保存場所の単位として認証情報とキーを管理します。キー保存場所がない場合は次のような画面が表示されます。

![console-guide-01](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-01.png)

**キー保存場所追加**をクリックすると、キーの保存場所を作成できるウィンドウが表示されます。

![console-guide-02](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-02.png)

名前と説明を入力し、1個以上の認証方法を選択した後、**追加**をクリックすると、キー保存場所を作成します。作成したキー保存場所は、次の図のようにキー保存場所リストに表示されます。

![console-guide-03](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-03.png)

キー保存場所リストでキー保存場所をクリックすると、次の図のようにキー保存場所を管理できるメニューが表示されます。

![console-guide-04](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-04.png)

### キーの作成
Secure Key Managerは、キーを3つのタイプに区分します。機密データは文字列データを保存し、APIを使用した照会機能を提供します。対称鍵はAPIを使用したデータ暗号化/復号機能を提供します。非対称鍵はAPIを使用したデータ署名/検証機能を提供します。ユーザーは使用目的に合ったキータイプを選択してキーを作成できます。

**キー管理**メニューをクリックすると、次の図のようにキーを管理できる画面が表示されます。

![console-guide-05](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-05.png)

キー管理画面で**キー追加**をクリックすると、キーを作成できるウィンドウが表示されます。選択したキーのタイプに応じて、自由にデータを入力できます。

![console-guide-06](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-06.png)


![console-guide-07](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-07.png)


![console-guide-08](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-08.png)


機密データを選択すると名前、説明、データを入力できます。対称鍵/非対称鍵を選択すると名前、説明、ローテーション周期を入力できます。必須データを入力した後、**追加**をクリックするとキーを作成します。作成したキーは次の図のようにキー管理画面に表示されます。

![console-guide-09](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-09.png)

### キーのインポート
Secure Key Managerは、対称鍵(AES-256)をインポートする機能をサポートします。

![console-guide-10](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-10.png)

**キーデータ**領域にキー値を入力してアップロードできます。アップロード可能なキーの形式は次のとおりです。

```
0xXX, 0xXX, ..., 0xXX
```

上記のように32個のHex Stringをカンマ(`,`)またはスペース(` `)で区切って入力してキーをアップロードします。

### 認証情報の登録
Secure Key Managerで作成したキーは、認証に成功したクライアントのみ使用できます。クライアント認証に使用する認証情報は**IPv4アドレス管理**、**MACアドレス管理**、**証明書管理**メニューで登録します。

#### IPv4アドレスの登録
**IPv4アドレス管理**をクリックすると、次の図のようにクライアント認証に使用するIPv4アドレス管理画面が表示されます。

![console-guide-11](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-11.png)

**IPv4アドレス追加**をクリックすると、図のようにIPv4アドレスを追加できるウィンドウが表示されます。

![console-guide-12](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-12.png)

IPv4アドレス追加**をクリックすると、図のようにIPv4アドレスを追加できるウィンドウが表示されます。

![console-guide-38](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2023-09-26-en/console-guide-38.png)

クライアントIPv4アドレスと説明を入力した後、**追加**をクリックすると、IPv4アドレスを追加します。この時、IPv4アドレスにはクライアントがSecure Key Managerに接続する時に使用するIPv4アドレスを入力する必要があります。追加したIPv4アドレスは次の図のようにIPv4アドレス管理画面に表示されます。

![console-guide-13](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-13.png)

#### MACアドレスの登録
**MACアドレス管理**をクリックすると、クライアント認証に使用するMACアドレス管理画面が表示されます。
![console-guide-14](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-14.png)

**MACアドレス追加**をクリックすると、MACアドレスを追加できるウィンドウが表示されます。

![console-guide-15](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-15.png)

クライアントMACアドレスと説明を入力した後、**追加**をクリックすると、MACアドレスを追加します。追加したMACアドレスはMACアドレス管理画面に表示されます。

![console-guide-16](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-16.png)

#### クライアント証明書の登録
**証明書管理**をクリックすると、クライアント認証に使用する証明書管理画面が表示されます。

![console-guide-17](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-17.png)

**証明書追加**をクリックすると、証明書を作成できるウィンドウが表示されます。

![console-guide-18](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-18.png)

証明書名、パスワード、説明を入力し、使用期間を選択した後、**追加**をクリックすると証明書を作成します。作成した証明書は次のように証明書管理画面に表示されます。証明書管理画面で**ダウンロード**アイコンをクリックすると証明書ファイルをダウンロードします。

![console-guide-19](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-19.png)

### ユーザーデータの管理
Secure Key Managerは、ユーザーが作成したデータ(キー、認証情報)の詳細情報を提供します。ユーザーデータリストで**詳細情報アイコン**をクリックすると、次の図のように詳細情報が表示されます。

![console-guide-20](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-20.png)

#### ユーザーデータの削除

ユーザーが作成したデータの初期状態は**使用中**です。不要なデータを削除するには次の図のように**詳細情報**ウィンドウで**削除リクエスト**をクリックします。

![console-guide-21](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-21.png)

削除をリクエストすると、次の図のようにデータ状態が**削除予定**に変更されます。**削除予定**に変更されたデータは使用できず、7日後に完全に削除されます。

![console-guide-22](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-22.png)

**削除予定**状態のデータは**即時削除**をクリックして削除予定時間まで待たずにすぐに削除することができます。また、**削除キャンセル**をクリックして**使用中**状態に戻すこともできます。

![console-guide-23](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-23.png)

#### 対称鍵/非対称鍵のローテーション

Secure Key Managerでは対称鍵/非対称鍵をローテーションできます。次の図のように対称鍵/非対称鍵詳細情報ウィンドウで自動ローテーション周期を設定できます。ローテーション周期を「0」に設定すると、自動ローテーションを行いません。

![console-guide-24](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-24.png)

ローテーション周期に30以上の値を設定すると、次のローテーション日を表示し、ローテーション周期ごとにキーを自動的にローテーションします。

![console-guide-25](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-25.png)

対称鍵/非対称鍵詳細情報ウィンドウで**即時ローテーション**をクリックすると、キーを即時にローテーションできます。

![console-guide-26](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-26.png)

キーをローテーションすると、次の図のようにキーバージョンリストに新しいバージョンが追加されます。

![console-guide-27](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-27.png)

例外としてキーのインポートを行って作成したキーはSecure Key Managerで作成した対称鍵とは異なり、ローテーション機能を提供しません。照会時、次のようにキーローテーション領域が存在しません。

![console-guide-28](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-28.png)

### 承認機能

#### 承認機能の有効化
組織管理画面のガバナンス設定で承認プロセス管理設定を利用してSecure Key Managerの承認機能を有効にします。

![console-guide-29](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-29.png)

#### 承認機能役割設定
Secure Key Managerのメンバー管理から承認者(APPROVAL ADMIN)、要請者(APPROVAL MEMBER)の役割を取得して承認手続きを進めます。

![console-guide-30](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-30.png)

#### 承認機能を有効にしたときの違い
承認機能を有効にして承認者または要請者の役割を取得すると、Secure Key Managerに**承認リスト**と**キー保存場所管理**タブが追加されます。2つのタブは承認者、要請者のみアクセスできます。

![console-guide-31](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-31.png)

承認機能を有効にすると、キー保存場所でデータを追加、修正、削除できなくなり、変更リクエストを行うと**キー保存場所管理**タブに移動します。

![console-guide-32](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-32.png)

#### 承認リクエスト作成
承認者と要請者は、**キー保存場所管理**タブでキー保存場所ごとに変更内容を承認リクエストできます。既存のキー保存場所と似た動作で追加、修正、削除を進めます。キー、認証情報の変更状態については次のように状態に表示されます。

![console-guide-33](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-33.png)

![console-guide-34](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-34.png)

キー保存場所の**承認リクエスト**ボタンで承認をリクエストし、該当プロジェクトの承認リクエストは**承認リスト**タブで確認できます。

![console-guide-35](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-35.png)

#### 承認リクエストの反映
承認者は、**承認リスト**からキー保存場所の変更承認リクエストを確認し、**承認**または**拒否**を選択して反映するかどうかを決定します。

![console-guide-36](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-36.png)

承認を押すとすぐにキー保存場所に反映されます。**キー保存場所**または**キー保存場所管理**タブで変更内容を確認できます。

![console-guide-37](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-37.png)

### キーの追加/削除API資格関連

#### User Access Key ID, Secret Access Key作成

コンソール右上のID領域をクリックすると、次のような**APIセキュリティー設定**メニューを確認できます。

![console-guide-38](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2023-11-28-en/console-guide-01.png)

**APIセキュリティー設定**で**User Access Key ID作成**をクリックしてSecure Key Managerキーの追加/削除APIに入力する必要がある**User Access Key ID**と**Secret Access Key**を生成できます。

![console-guide-39](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2023-11-28-en/console-guide-02.png)

![console-guide-40](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2023-11-28-en/console-guide-03.png)

**User Access Key ID**、**Secret Access Key**を生成すると、下記のように**シークレットキー発行完了**画面が表示されます。秘密鍵はそのポップアップ画面で一度だけ教えてくれるので、この値をよく記録して使います。

![console-guide-41](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2023-11-28-en/console-guide-04.png)

APIリクエスト時に必要な**User Access Key ID**は秘密鍵発行完了ポップアップを閉じると確認できます。

![console-guide-42](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_kms/2023-11-28-en/console-guide-05.png)
