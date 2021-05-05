---
title: サーバー エクスプローラーから Azure Virtual Machines へのアクセス | Microsoft Docs
description: Visual Studio のサーバー エクスプローラーで Azure Virtual Machines (VM) を作成したり管理したりする方法について簡単に説明します。
author: ghogen
manager: jmartens
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 8/31/2017
ms.author: ghogen
ms.openlocfilehash: a40434845187490ee4f8437f8e15963bddd1998f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99843788"
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>サーバー エクスプローラーから Azure Virtual Machines へのアクセス

Azure でホストされている仮想マシンには、サーバー エクスプローラーでアクセスできます。 まず Azure サブスクリプションにサインインして、ご利用の Mobile Services を表示してください。 サインインするには、サーバー エクスプローラーで Azure ノードのショートカット メニューを開き、 **[Microsoft Azure への接続]** をクリックします。

1. Cloud Explorer で仮想マシンを選択し、F4 キーを押してプロパティ ウィンドウを表示します。

    次の表に示したのは、アクセスできるプロパティの一覧です。ただし、これらはすべて読み取り専用です。 これらのプロパティを変更するには、[Azure Portal](https://portal.azure.com) を使用します。

   | プロパティ | 説明 |
   | --- | --- |
   | DNS 名 |仮想マシンのインターネット アドレスを含む URL。 |
   | 環境 |仮想マシンの場合、このプロパティの値は常に [運用] です。 |
   | 名前 |仮想マシンの名前。 |
   | サイズ |仮想マシンのサイズ。使用できるメモリとディスク領域のサイズが反映されます。 詳細については、[仮想マシンのサイズ](/azure/cloud-services/cloud-services-sizes-specs)に関する記事をご覧ください。 |
   | Status |"開始中"、"開始"、"停止中"、"停止"、"状態を取得中" などの値があります。 "状態を取得中" と表示された場合、現在の状態は不明です。 このプロパティの値は、[Azure Portal](https://portal.azure.com) で使用される値とは異なります。 |
   | SubscriptionID |ご利用の Azure アカウントのサブスクリプション ID。 この情報を [Azure Portal](https://portal.azure.com) に表示するには、サブスクリプションのプロパティを表示します。 |
2. エンドポイント ノードを選択し、**[プロパティ]** ウィンドウを表示します。
3. 次の表は、エンドポイントに関してアクセスできるプロパティの説明です。これらは読み取り専用となります。 仮想マシンのエンドポイントを追加または編集するには、[Azure Portal](https://portal.azure.com) を使用します。

   | プロパティ | 説明 |
   | --- | --- |
   | 名前 |エンドポイントの ID。 |
   | プライベート ポート |アプリケーションの内部ネットワーク アクセス用ポート。 |
   | Protocol |このエンドポイントのトランスポート レイヤーで使用されるプロトコル (TCP または UDP)。 |
   | パブリック ポート |アプリケーションに外部からアクセスする際に使用するポート。 |
