---
title: 全般 タブで、処理のプロパティ ダイアログ ボックス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: 86f4d61d-a594-4aac-8960-c5279b4a10fd
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9256ca4141e9e4ec9e5ae218f1e5a11bf2fa5362
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68182293"
---
# <a name="general-tab-process-properties-dialog-box"></a>[全般] タブ ([プロセス プロパティ] ダイアログ ボックス)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用して、**全般**特定のプロセスに関する詳細はタブ。 表示する、[プロセス プロパティ ダイアログ ボックス](../debugger/process-properties-dialog-box.md)、フォーカスを移動、[プロセス ビュー](../debugger/processes-view.md)ウィンドウ。 ツリーで、プロセスの任意のノードを選択し、**プロパティ**から、**ビュー**メニュー。  
  
 次の設定は [使用可能な**全般**] タブ。  
  
|入力|説明|  
|-----------|-----------------|  
|**モジュール名**|モジュールの名前です。|  
|**プロセス ID**|このプロセスの一意の ID。 そのプロセスの有効期間のみのプロセスを識別できるように、プロセス ID 番号が再利用されます。 プログラムの実行時にプロセス オブジェクトの種類が作成されます。 プロセス内のすべてのスレッドが同じアドレス領域を共有し、同じデータにアクセスします。|  
|**ベースの優先度**|このプロセスの現在の基本優先順位。 プロセス内のスレッドは、発生させるし、プロセスの基本優先順位を基準とした独自の基本優先順位を下げます。|  
|**スレッド**|このプロセスで現在アクティブなスレッドの数。|  
|**CPU 時間**|総 CPU 時間は、このプロセスとそのスレッドに費やされました。 ユーザーの時間と特権モード時間等しい。|  
|**ユーザー モード時間**|このプロセスのスレッドが非アイドルのスレッドでユーザー モードでコードの実行に費やさ累積的な経過時間。 アプリケーションは、ウィンドウ マネージャーおよびグラフィックス エンジンなどのサブシステムと同様に、ユーザー モードで実行されます。|  
|**特権モード時間**|経過時間の合計このプロセスの実行特権モードで非アイドルのスレッドでします。 サービス層、Executive ルーチン、およびカーネルを特権モードで実行します。 グラフィックス アダプターとプリンター以外のほとんどのデバイスのデバイス ドライバーは特権モードでも実行します。 特権モード時間に加えて他のサブシステム プロセスで、アプリケーションの Windows をいくつかの作業があります。|  
|**経過時間**|このプロセスの実行経過時間の合計。|
