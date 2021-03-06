﻿##　操作シナリオ
TencentDB for Redis クラスタ版（コミュニティ）にはインスタンスのクローン作成機能があり、バックアップファイルに基づいて完全な新しいインスタンスを複製することができます。インスタンスのデータとバックアップファイルが同じである場合、クローン機能を利用して以前のデータを分析することができます。また、IP を変更してクローンの新インスタンスと旧インスタンスの IP を交換することで復旧を行うことも可能です。

## 前提条件
インスタンスデータをバックアップしていることが必要です。バックアップの操作については、[データのバックアップ](https://cloud.tencent.com/document/product/239/30901)を参照してください。

## 操作手順
1. [Redis コンソール](https://console.cloud.tencent.com/redis)にログインし、インスタンスリストでインスタンス名をクリックしてインスタンスの詳細ページに移動します。
2. 【バックアップとリカバリ】ページでクローン作成が必要なインスタンスを選択し、【インスタンスのクローン作成】をクリックします。
![](https://main.qcloudimg.com/raw/262eb6918a00e2eee4f796decb0d14f4.png)
3. ポップアップされた購入ページで関連パラメータを設定し、【すぐに買う】をクリックします。
4. インスタンスリストに戻り、インスタンスのステータスが【実行中】になれば正常に使用できます。
>?インスタンスのクローン作成後、旧インスタンスはユーザーの必要に応じてそのまま残したり、破棄したりすることができます。



