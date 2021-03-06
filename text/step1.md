■VPCとパブリックサブネットの作成
===

 [VPCとは](http://docs.aws.amazon.com/ja_jp/AmazonVPC/latest/UserGuide/VPC_Introduction.html)
### VPCと一つのサブネットを作成

[VPCとサブネット](http://docs.aws.amazon.com/ja_jp/AmazonVPC/latest/UserGuide/VPC_Subnets.html)

1. マネジメントコンソールにアクセス、VPCダッシュボードへ移動
2. VPC作成ウィザードを起動
3. 「1 個のパブリックサブネットを持つ VPC」を選択
4. VPCの設定とパブリックサブネットの設定
  * VPC名：**[チーム名]-wp-practice**
  * VPCのCIDR：**10.0.0.0/16**
    * -> 10.0.0.0〜10.0.255.255の範囲を持つネットワーク
  * パブリックサブネットのCIDR：**10.0.1.0/24**
    * -> 10.0.0.0/16に属し、10.0.1.0〜10.0.1.255の範囲を持つネットワーク
  * サブネット名：**[チーム名]-パブリックサブネット**
  * ほかデフォルト

### パブリックサブネットをインターネットに接続

[インターネットゲートウェイ](http://docs.aws.amazon.com/ja_jp/AmazonVPC/latest/UserGuide/VPC_Internet_Gateway.html)

1. VPCダッシュボード ->「サブネット」->「[チーム名]-パブリックサブネット」を選択
2. ルートテーブルタブを選択し、「rtb-xxxxxxxx」のリンクを選択
3. ルートテーブルの設定を確認
  * 10.0.0.0/16：local
  * 0.0.0.0/0：igw-xxxxxxxx（インターネットゲートウェイのID）
    * VPC内のアドレス範囲以外はインターネットへ流す設定（デフォルトゲートウェイ）

#### ★VPCの利用料金
VPC自体の利用に関しては無料。VPC内で起動したEC2などの料金は別途EC2として課金される。
VPN接続を利用する場合はその接続時間に応じて課金される。

#### ★サブネットの切り方ってどう考えりゃ良いの？
[AWSのネットワーク設計をサボらないでちゃんとやる - Qiita](http://qiita.com/nisshiee/items/df4261132ec686964605)
