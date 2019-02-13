---
title: サーバー エクスプローラーから Azure Virtual Machines へのアクセス | Microsoft Docs
description: Visual Studio のサーバー エクスプローラーで Azure Virtual Machines (VM) を作成したり管理したりする方法について簡単に説明します。
author: ghogen
manager: jillfra
assetId: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 8/31/2017
ms.author: ghogen
ms.openlocfilehash: e4f8f72dcc19ebe721e79c7b5268fd73d2cc469e
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55930832"
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>サーバー エクスプローラーから Azure Virtual Machines へのアクセス

Azure でホストされている仮想マシンには、サーバー エクスプローラーでアクセスできます。 まず Azure サブスクリプションにサインインして、ご利用の Mobile Services を表示してください。 サインインするには、サーバー エクスプローラーで Azure ノードのショートカット メニューを開き、 **[Microsoft Azure への接続]** をクリックします。

1. Cloud Explorer で仮想マシンを選択し、F4 キーを押してプロパティ ウィンドウを表示します。

    次の表に示したのは、アクセスできるプロパティの一覧です。ただし、これらはすべて読み取り専用です。 これらのプロパティを変更するには、[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) を使用します。

   | プロパティ | 説明 |
   | --- | --- |
   | DNS 名 |仮想マシンのインターネット アドレスを含む URL。 |
   | 環境 |仮想マシンの場合、このプロパティの値は常に [運用] です。 |
   | name |仮想マシンの名前。 |
   | サイズ |仮想マシンのサイズ。使用できるメモリとディスク領域のサイズが反映されます。 詳細については、[仮想マシンのサイズ](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs)に関する記事をご覧ください。 |
   | Status |"開始中"、"開始"、"停止中"、"停止"、"状態を取得中" などの値があります。 "状態を取得中" と表示された場合、現在の状態は不明です。 このプロパティの値は、[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) で使用される値とは異なります。 |
   | SubscriptionID |ご利用の Azure アカウントのサブスクリプション ID。 この情報を [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) に表示するには、サブスクリプションのプロパティを表示します。 |
2. エンドポイント ノードを選択し、 **[プロパティ]** ウィンドウを表示します。
3. 次の表は、エンドポイントに関してアクセスできるプロパティの説明です。これらは読み取り専用となります。 仮想マシンのエンドポイントを追加または編集するには、[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) を使用します。

   | プロパティ | [説明] |
   | --- | --- |
   | name |エンドポイントの ID。 |
   | プライベート ポート |アプリケーションの内部ネットワーク アクセス用ポート。 |
   | プロトコル |このエンドポイントのトランスポート レイヤーで使用されるプロトコル (TCP または UDP)。 |
   | パブリック ポート |アプリケーションに外部からアクセスする際に使用するポート。 |
