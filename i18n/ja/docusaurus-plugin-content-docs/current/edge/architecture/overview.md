---
id: overview
title: アーキテクチャの概要
sidebar_label: Overview
description: Polygon Edgeのアーキテクチャの紹介。
keywords:
  - docs
  - polygon
  - edge
  - architecture
  - modular
  - layer
  - libp2p
  - extensible
---

まず*モジュラー*であるソフトウェアを作るというアイデアから始まりました。

これはPolygon Edgeのほぼすべての部分に存在するものです。下記の簡単な概要は構築されたアーキテクチャとそのレイヤーに関するものです。

## Polygon Edgeのレイヤー {#polygon-edge-layering}

![Polygon Edgeアーキアーキテクチャ](/img/edge/Architecture.jpg)

## Libp2p {#libp2p}

すべてベースネットワークレイヤーから始まりますが、これは**libp2p**を活用します。この技術を用いることを決めました。その理由は、これがPolygon Edgeの設計哲学に適合するからです。Libp2pは以下のとおりです：

- モジュール式
- 拡張可能
- 高速

最も重要なのは、それがより高度な機能のために優れた基盤を提供することですが、これは後ほどカバーします。


## 同期とコンセンサス {#synchronization-consensus}
同期とコンセンサスのプロトコルの分離により、クライアントの実行方法次第で、モジュール化と**カスタム**同期、コンセンサス方式の導入が可能になります。

Polygon Edgeは既存のプラグ可能なコンセンサスアルゴリズムを提供するよう設計されています。

現在サポートしているコンセンサスアルゴリズムのリスト：

* IBFT PoA
* IBFT PoS

## ブロックチェーン {#blockchain}
ブロックチェーンレイヤーはPolygon Edgeシステムのすべてを調整する中央レイヤーです。これは付随する*モジュール*セクションで詳しく取り上げています。

## ステート {#state}
ステート内部レイヤーはステート移行ロジックを含みます。新しいブロックが含まれる時にステートがどのように変化するかに対応します。これは付随する*モジュール*セクションで詳しく取り上げています。

## JSON RPC {#json-rpc}
JSON RPCレイヤーはdApp開発者がブロックチェーンとやり取りするために使用するAPIレイヤーです。これは付随する*モジュール*セクションで詳しく取り上げています。

## TxPool {#txpool}
TxPoolレイヤーはトランザクションプールを表し、トランザクションが複数のエントリーポイントから追加できるためにシステム内の他のモジュールと密接にリンクしています。

## grpc {#grpc}
gRPC（googleリモートプロシージャコール）は、Googleが最初に作成した堅牢なオープンソースRPCフレームワークです。GRPCレイヤーはオペレータのやり取りに重要です。これを通じてノードオペレータはクライアントと簡単にやり取りできるため、楽しめるUXを提供します。