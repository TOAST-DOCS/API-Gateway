## Application Service > API Gateway > API Gatewayクライアントファイアウォールポリシー設定 

### API Gatewayクライアントファイアウォールポリシー設定 

クライアントがAPI Gatewayを通じて提供されるAPIを呼び出す時、ファイアウォール(Network ACL)を使用する場合、正常な通信のためにAPI Gateway VIPに対するファイアウォールポリシーを設定する必要があります。
API Gateway VIPに対するファイアウォールポリシー設定がない場合、ドメインの問い合わせ結果によってAPI呼び出しに失敗する可能性があります。
クライアントがファイアウォールを別途に管理していない場合は、特別な処理なしで使用可能です。

#### API Gateway VIP情報

| VIP | ポート |
| --- | --- |
| 180.210.64.24<br>180.210.65.24<br>180.210.64.224<br>180.210.65.224<br>117.52.123.41<br>114.110.141.140 | 80,443 |

API Gateway VIP情報を参考にして、次のファイアウォール(Network ACL)を設定してください。
* 出発地：API Gatewayを通じて提供されるAPIを呼び出すクライアントIP
* 宛先：API Gateway VIPリスト全体 
* ポート：80,443
* 通信ポリシー：許可(Allow) 

> **[参考]** API Gateway VIP変更
> * API Gateway VIPリストは、事前告知後に変更される場合があります。
> * 変更時、変更内容を確認した後、変更されたVIPに対するファイアウォールポリシーを設定する必要があります。