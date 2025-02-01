##
 SuperchainERC
20: 資産相互運用性を実現する革新的なERC-20
規格

**SuperchainERC20** は、Superchain内での資産
相互運用性を可能にするために**ERC-7802**を実装した、革新的なERC-20規格です。

### SuperchainERC2
0とは？

SuperchainERC20は、トークンがSuperchain内の異なるチェーン間を安全に移動することを可能にする規格です。従来の
資産ラッピングや流動性プールの利用に比べて、**ソースチェーンでトークンをバーンし、デスティネーションチェーンで同等のトークンをミントする**というシンプルな仕組みを採用することで、流動性
断片化やユーザーエクスペリエンスの悪化といった問題を解決します。

### SuperchainERC20の利点

* **資産の相互運用性:** トークンをSuperchain内の異なるチェーン間で安全に
移動させることができます。
* **流動性向上:** 複数のチェーンに分散した流動性を集約することで、流動性を向上させます。
* **ユーザーエクスペリエンスの向上:** 複雑なラッピングやブリッジングの手順を省略することで、ユーザーエクスペリエンスを向上
させます。
* **簡素化された導入:** 導入に特別なインフラストラクチャは不要です。
* **共通規格:** ERC-7802の実装により、Ethereumエコシステム全体で共通のインターフェースを提供します。

### SuperchainERC20の仕組み

Superchain
ERC20は、**SuperchainTokenBridge**と連携して、ERC-20トークンのチェーン間転送を実現します。

1. **初期化メッセージ（ソースチェーン）**
    * ユーザーまたはコントラクトがSuperchainTokenBridge.sendERC20を呼び出します。

    * SuperchainTokenBridgeは、ソースチェーンでSuperchainERC20.crosschainBurnを呼び出してトークンをバーンします。
    * ソースチェーンのトークンブリッジは、デスティネーションチェーンのSuperchainTokenBridge.relayERC20を呼び出します。この呼び出しは
、L2ToL2CrossDomainMessengerを使用して中継されます。

2. **実行メッセージ（デスティネーションチェーン）**
    * ユーザーまたはリレーヤーが、L2ToL2CrossDomainMessengerに実行メッセージを送信して中継します。
    * デスティネーションチェーンの
トークンブリッジは、SuperchainERC20.crosschainMintを呼び出して、元のSuperchainTokenBridge.sendERC20を呼び出したユーザーまたはコントラクトにトークンをミントします。

### SuperchainERC20への対応

SuperchainERC20に対応するには、アプリケーション開発者は
以下の2つの手順を実行する必要があります。

1. **SuperchainTokenBridgeへの権限付与:** SuperchainTokenBridge (アドレス: 0x42000000000000000000000000000000000
00028) がcrosschainMintおよびcrosschainBurnを呼び出す権限を付与します。SuperchainERC20を使用している場合は、すでに設定されています。

2. **ERC-20コントラクトのデプロイ:** Superchain内のすべてのチェーンで、同じアドレスにERC-20
コントラクトをデプロイします。create2を使用すると簡単です。

**セキュリティ上の注意:**

不正なERC-20コントラクトがSuperchainネットワーク上の同じアドレスにデプロイされると、悪意のある者が無制限にトークンをミントして、元のERC-20コントラクト
が存在するネットワークにブリッジできる可能性があります。そのため、デプロイヤーは、SuperchainERC20などの信頼できる特定のERC-20コントラクトのみがデプロイされるように設計するか、または、CREATE2を使用して制御するEOAから直接コントラクトをデプロイする必要があります。

###
 まとめ

SuperchainERC20は、Superchain内の資産相互運用性を向上させる画期的な規格です。トークンの相互運用性を強化することで、Superchain全体での流動性とユーザーエクスペリエンスを大幅に向上させることが期待されます。

### 今後の展開

* SuperchainERC
20の動画チュートリアルで、既存のERC-20コントラクトをSuperchainに対応させる方法を学ぶことができます。
* SuperchainERC20の仕様で、実装の詳細を確認することができます。
* SuperchainERC20スターターキットで、実装を始めることができます。
