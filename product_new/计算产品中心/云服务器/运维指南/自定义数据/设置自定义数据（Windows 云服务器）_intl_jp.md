## 操作シナリオ

CVMを作成する時に、**カスタムデータ**を指定することでインスタンスを構成できます。CVMを**初回起動**する時に、カスタムデータがテキスト形式でCVMに渡され、実行されます。一度に複数台のCVMを購入する場合、カスタムデータは、すべてのCVMの初回起動時にこのテキストを実行します。
本書では、Windows CVMの初回起動時に、PowerShell形式のスクリプトを渡すのを例として説明します。

## 注意事項

- カスタムデータをサポートするWindows OSには次のものが含まれています。
 - Windows Server 2016 データセンター版 64ビット 中国語/英語版
 - Windows Server 2012 R2 データセンター版 64ビット 中国語/英語版
- CVMの初回起動時のみ、テキストを渡すことでコマンドを実行します。
- カスタムデータのコンテンツは、Base64コーディングの前に16KBを超えてはいけません。
- カスタムデータはBase64コーディングで渡されます。base64以外のスクリプトファイルを直接コピーする場合は、【base64形式のテキストとして入力】を選択しないでください。
- 起動時に、カスタムデータで指定されたタスクを実行すると、サーバーの起動時間が長くなります。数分間待ってから、タスクが完了した後にタスクが正常に実行されたかどうかをテストすることをお勧めします。
- この例では、&lt;powershell&gt;&lt;/powershell&gt;タグなどのPowerShellタグを使用してWindows PowerShellスクリプトを指定してください。

## 操作手順

### テキストを準備する

実際のニーズに応じてテキストを準備してください。

<span id="PowerShellScript"></span>
#### PowerShell スクリプト
PowerShellタグを使用して、1つのPowerShellスクリプトファイルを準備します。
たとえば、CVMのC:ドライブでコンテンツが「Hello Tencent Cloud．」である「tencentcloud.txt」ファイルを作成する必要がある場合、PowerShellタブを使用して次の内容を準備できます。
```
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```

<span id="Base64Script"></span>
#### Base64コーディングスクリプト

1.次のコマンドを実行して、「script_text.ps1」という名前の PowerShellスクリプトファイルを作成します。
```
vi script_text.ps1
```
2. **i**または**Insert**を押して編集モードに切り換え、下記を参照して、「script_text.ps1」スクリプトファイルを書き込んで保存します。
```
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```
1. 次のコマンドを実行して、「script_text.ps1」スクリプトファイルに対してBase64エンコーディング操作を実行します。
```
base64 script_text.ps1
```
次の情報が返されます。
```
PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAgQzpcdGVuY2VudGNsb3VkLnR4dAo8L3Bvd2Vyc2hlbGw+Cg==
```

### テキストを渡す

インスタンスを起動するさまざまな方法が提供されます。主に次の2つの方法があり、実際のニーズに応じて選択してください。
- [公式サイトまたはコンソールによって渡す](#Consoletrans)
- [APIによって渡す](#APItrans)

<span id="Consoletrans"></span>
#### 公式サイトまたはコンソールによって渡す

1. [インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855) を参照してインスタンスを購入します。また「4.セキュリティグループとホストの設定」で[詳細設定]をクリックします。
2. 「詳細設定」では、実際のニーズに応じて、「カスタムデータ」のテキストボックスに用意されたテキスト内容を入力します。
 - PowerShellスクリプト：[PowerShell スクリプト](#PowerShellScript)を直接入力します。
 - Base64コーディングスクリプト：先に【base64形式のテキストとして入力】にチェックを入れてから、[Base64 コーディングスクリプト](#Base64Script)を入力する必要があります。
3.画面情報に従って逐次に操作し、CVMの作成を完了します。

<span id="APItrans"></span>
#### APIによって渡す

APIを介してCVMを作成する場合、[Base64コーディングスクリプト](＃Base64Script)で返されたコーディング結果をRunInstancesインターフェースのUserDataパラメータに代入することにより、テキストを渡すことができます。
たとえば、UserDataパラメータ付きのCVMのリクエストパラメータを作成する場合、例は次のとおりです。
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAuXHRlbmNlbnRjbG91ZC50eHQKPC9wb3dlcnNoZWxsPgo=
  &<パブリックリクエストパラメータ>
```

### カスタムデータの設定を検証する

1. CVMにログインします。
2. OS画面で、 C:ドライブを開き、「tencentcloud.txt」テキストファイルがあるかどうかを確認します。
「tencentcloud.txt」テキストファイルがあると確認できた場合、設定が成功です。


