CDNサービスにアクセスしたドメイン名に対し、 HTTPS 証明書の設定を行うことができます。CDNサービスは既存証明書、またはTencent Cloud[SSL証明書管理](https://console.cloud.tencent.com/ssl)  コンソールにおけるホスティング証明書又は発行証明書の設定をサポートしています。
>証明書は期限切れの30日前、15日前、7日前及び期限切れの当日には、Tencent Cloudはsms、メール、内部メールの形式でユーザーのアカウントへ満期注意を送信します。現在、SSL証明書のアラーム受信者のカスタマイズを対応しています。ユーザーは [メッセージサブスクリプション](https://console.cloud.tencent.com/message/subscription) に入り設定することが可能です。

## 証明書及びプライベートキー
ドメイン名に既存証明書を設定する場合は、まず下記内容を理解してください。
>Tencent Cloud [SSL 証明書管理](https://console.cloud.tencent.com/ssl) コンソールにおけるホスティング証明書又は発行証明書を設定している場合は、この部分の内容をスキップし、直接に次の [証明書設定](#configuration) 手順をご参照ください。


CA機構によって提供する証明書は一般的に下記の幾つかの種類を含んでいます。その中に、CDNサービスは**Nginx**を使用します。


![](https://main.qcloudimg.com/raw/a2c1b413f9cf770cf7facdb3e424eac4.png)


Nginxフォルダーに入り、テキストエディッターを使用して「.crt」（証明書）ファイルと 「.key」（プライベートキー）ファイルを開くと、PEMフォーマットの証明書内容及びプライベートキーの内容を確認することができます。


![](https://main.qcloudimg.com/raw/26bf3f290b85ea75c3a4d74f66334d55.png)

### 証明書
証明書の拡張子は一般的に「.pem」、「.crt」又は「.cer」です。テキストエディッターを使用して証明書ファイルを開くと、下記図に類似している証明書内容を確認することができます。
証明書PEMフォーマット：「-----BEGIN CERTIFICATE-----」を先頭、「-----END CERTIFICATE-----」を末尾とします。内容は1行あたり64文字で、最後の行の長さが64文字未満にすることができます。


![](https://main.qcloudimg.com/raw/60ea02d1a2c9623526d7fa79403e658a.jpg)


証明書が中級CA機構によって発行された場合、入手している証明書ファイルに複数の証明書が含まれており、サーバー証明書と中間証明書を組み合せてからアップロードする必要があります。組み合せのルールは下記の通りです。サーバー証明書は1部目、中間証明書は2部目であり、その間に空行があってはなりません。一般的には、機構が証明書を発行する時に、対応する説明がありますので、ルールの説明をよく確認してください。
>
>- 証明書の間に空行があってはなりません。
>- 各証明書のフォーマットはPEMフォーマットです。

中級機構により発行する証明書チェーンのフォーマットは下記の通りです。
```
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
```
### プライベートキー
プライベートキーの拡張子は一般的に「.pem」又は「.key」です。テキストエディッターを使用してプライベートキーファイルを開くと、次図のフォーマットに類似するプライベートキーの内容を確認することができます。 
プライベートキーPEMフォーマット：「-----BEGIN RSA PRIVATE KEY-----」を先頭、「-----END RSA PRIVATE KEY-----」を末尾とします。その間の内容は1行あたり64文字であり、最後の行の長さが64文字未満にすることができます。


![](https://main.qcloudimg.com/raw/e10009916aeb00d5158a3703115d0354.jpg)


「-----BEGIN PRIVATE KEY-----」を先頭、「-----END PRIVATE KEY-----」を末尾とするプライベートキーを取得する場合は、opensslツールによりフォーマットを変換することをお勧めします。コマンドは下記の通りです。
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```

<span ID ="configuration"></span>
## 証明書設定
1.  [CDNコンソール ](https://console.cloud.tencent.com/cdn)にログインし、左側のメニュー欄の【certificate  】をクリックして、証明書管理ページに入ります。
2. 【Configure Certificate】をクリックし、証明書設定ページに入ります。


 ![](https://main.qcloudimg.com/raw/e72970f28fc8539eb1317ad24a41bbcb.png)


### ドメイン名の選択
【Domain】のプルダウンメニューから設定しようとする証明書のドメイン名を選択します。
![証明書のドメイン名](https://main.qcloudimg.com/raw/4288a4be379e61addc777b3c3d017ebf.png)


>
> + 証明書のドメイン名を設定するにはTencent Cloud CDNサービスに接続し、且つドメイン名の状態は**デプロイ中**又は**起動済み**にある必要があります。**無効になっている**状態にあるドメイン名は証明書をデプロイすることができません。
> + Tencent Cloudの**Cloud Object Storage**又は**Cloud YouTu**サービスを利用し、 CDN 加速を有効にすると、デフォルトの `.file.myqcloud.com` 又は `.image.myqcloud.com` ドメイン名は証明書を設定することができません。

### 証明書の選択
自分の証明書又はTencent Cloudのホスティング証明書を使用することを選択できます。
#### 自己証明書
【Self-owned Certificate】を選択し、証明書の内容とプライベートキーの内容をテキストボックスに貼り付けます。証明書に対し備考情報を追加することにより区分けすることができます。
![証明書を選択する](https://main.qcloudimg.com/raw/6ee06763e595b9739407d295194c0b61.png)


>
> + 証明書の内容はPEM フォーマットである必要があります。当該フォーマットでない証明書については、以下の **PEMフォーマット変換**内容を参考してください。
> + 証明書は証明書チェーンがある場合、証明書チェーンの内容をPEMフォーマットの内容に変換し、証明書の内容と合わせてからアップロードしてください。証明書チェーンの補完については、以下の内容**証明書チェーンの補完**を参考してください。

#### Tencent Cloudホスティング証明書
 [SSL 証明書管理](https://console.cloud.tencent.com/ssl) コンソールにログインしたり、TrustAsiaによる無料提供のサードパーティーの証明書を申請したり、既存証明書をTencent Cloudにホスティングしたりすることが可能です。
【Tencent Cloud hosted Certificate】を選択すると、当該ドメイン名で利用可能な証明書リストを確認することができます。証明書リストから使用する証明書を選択します。証明書リストには証明書が「証明書 ID（備考）」の様式で表示されています。

### back to origin方法
証明書を設定した後に、CDNノードがオリジンサーバーからリソースを取得する時のback to origin方法を選択することができます。CDNサービスは**HTTP** 及び**プロトコルback to origin**という2種類のback to origin方法を対応しています。


![](https://main.qcloudimg.com/raw/719036689548a629283069a4a796156a.png)

>
> +  **HTTP**back to origin方式を選択して成功に設定した後に、CDNノードへのユーザーリクエストはHTTPS/HTTPをサポートします。オリジンサーバーへのCDNノードのリクエストは全部HTTPです。
> + **プロトコルフォロー**のback to origin設定を選択する場合は、オリジンサーバーに有効な証明書がデプロイされている必要があります。そうでない場合、back to originの失敗が発生します。成功に設定した後に、CDNノードへのユーザーリクエストがHTTPである場合、CDNノードのback to originリクエストもHTTPとなります。CDNノードへのユーザーリクエストがHTTPSである場合、CDNノードのback to originリクエストもHTTPSとなります。
> + ドメイン名のオリジンサーバーがHTTPSポートを443以外のポートに変更する場合は、設定の失敗が発生します。
> + COS オリジン又はFTP オリジンドメイン名は HTTP　back to originしか対応していません。

#### 成功に設定する
【Trending】をクリックすると、【Certificate Management】ページで成功に設定したドメイン名及び証明書情報を確認することができます。
![証明書構成の成功リスト](https://main.qcloudimg.com/raw/1e3b016e129c9d3f5e311fb9440b2b70.png)

## 証明書の一括設定
マルチドメイン名証明書又は汎用ドメイン名証明書を持っている場合は、複数のCDN加速ドメイン名に適しています。一括設定により、複数のドメイン名の設定を一度に追加することができます。
1.  [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のメニュー欄の【Certificate】をクリックすると、証明書管理ページに入ります。
2. 【Batch Configuration】をクリックすると、一括管理ページに入ります。


 ![](https://main.qcloudimg.com/raw/03f34e25c7c2a877fc0dfb3d93b80ee2.png)

### 証明書をアップロードする
PEMエンコードの証明書内容及びプライベートキーを対応するのテキストボックスに貼り付けます。備考名の変更により設定された証明書をマークすることができます。それから【Next】をクリックします。

![一括](https://main.qcloudimg.com/raw/e01b281accc7f413ced65bc3061d23b5.png)


### ドメイン名の関連付け及びback to origin方法の選択
CDNサービスシステムはアップロードされた証明書を利用できるCDN加速ドメイン名（ドメイン名は**デプロイ中**又は**起動済み**の状態にある必要がある）を識別することができます。ユーザーは、関連付ける必要があるドメイン名、及びback to origin方法を選択することができます。
![一括2](https://main.qcloudimg.com/raw/5af0cdca96bb92488a05d0e8474a7dad.png)


>
> + 1回当りは最大で10個の加速ドメイン名を選択し設定することが可能です。
> +  **HTTP** back to origin方式を選択し、成功に設定した後に、 CDNノードへのユーザーリクエストがHTTPS/HTTPをサポートします。オリジンサーバーへのCDNノードのリクエストは全部HTTPです。
> +  **プロトコルフォロー**のback to origin設定を選択する場合は、オリジンサーバーに有効な証明書をデプロイされている必要があります。そうでない場合、back to originの失敗が発生します。成功に設定した後に、CDNノードへのユーザーリクエストがHTTPである場合、CDNノードのback to originリクエストもHTTPとなります。CDNノードへのユーザーリクエストがHTTPSである場合、CDNノードのback to originリクエストもHTTPSとなります。
> + 一括選択されたドメイン名の中では、オリジンサーバーがHTTPSポートを443以外のポートに変更したものがあれば、設定の失敗を引き起こします。
> + 一括選択されたドメイン名の中では COS オリジン又は FTP オリジンのドメイン名が存在する場合、 HTTP back to origin しか対応しません。

### 設定の提出
【Trending】をクリックすると、CDNサービスは選択されたドメイン名に対し証明書を設定します。各ドメイン名の設定には5分間がかかりますので、しばらくお待ちください。ユーザーは【Certificate Management】ページで証明書の設定状態を確認することができます。
>
> + 設定が失敗した場合は、ドメイン名の右側にある【Edit】ボタンをクリックし、証明書の設定を再度実行できます。
> + 一括設定されたドメイン名には証明書を設定したドメイン名ががある場合、当該操作はドメイン名の元証明書を上書きします。上書きに失敗した場合、当該ドメイン名の証明書状態は【Update failed】になります。この場合、最初に設定した証明書がまだ有効です。ドメイン名の右側の【Edit】ボタンをクリックすることにより、上書き操作を再開することができます。

## 証明書の編集
成功に設定した証明書に対し、ドメイン名の右側の【Edit】ボタンをクリックすることにより証明書を更新することができます。
![証明書の編集](https://main.qcloudimg.com/raw/0c5d408ac629a39135ed784eb6749bbe.png)
独自の証明書とTencent Cloudホスティング証明書の間に切り替えたり、back to origin方法を選択しなおしたりすることができます。【submit】をクリックするとデプロイが完了されます。デプロイプロセスはシームレスに上書きであり、ビジネスでの使用には影響しません。

## 証明書の削除
ドメイン名の右側にある【setRegion】ボタンをクリックすることにより、CDNサービスにデプロイされた証明書を削除することができます。
![証明書の削除](https://main.qcloudimg.com/raw/49df665ca44fb4858f312e050d32b6eb.png)

## 証明書チェーンの補完
自分の証明書を設定する過程では、**証明書チェーンが補完できない**という場合があります。
CAの証明書（PEM フォーマット）の内容をドメイン名証明書（PEM フォーマット）の最後に貼り付けることにより、証明書チェーンを補完することができます。また、チケットを提出して弊社に連絡することもできます。
![](https://main.qcloudimg.com/raw/cf66482b81b4aae1e0a943c984243f1d.png)

## PEM フォーマットの変換
現在、CDNサービスはPEMフォーマットの証明書をしか対応していません。ほかのフォーマットの証明書は PEM フォーマットに変換する必要があります。opensslツールを使用して変換することをお勧めします。下記はよく使われている、証明書フォーマットを PEM に変換するの方法です。

### DERをPEMに変換する
DERフォーマットは一般的にJavaプラットホームに使われています。
証明書の変換：
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
プライベートキーの変換：
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```

### P7BをPEMに変換する
P7Bフォーマットは一般的にWindows Server 及び tomcat に使われています。
証明書の変換：
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
テキストエディッターでoutcertificat.cerを開くと、PEMフォーマットの証明書内容を確認することができます。
プライベートキーの変換：プライベートキーは一般的に IISサーバーでエクスポートされることが可能です。

### PFXをPEMに変換する
PFXフォーマットは一般的にWindows Serverに使われています。
証明書の変換：
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
プライベートキーの変換：
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```
