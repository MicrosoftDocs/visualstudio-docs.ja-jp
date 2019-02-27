---
title: チャネル (スレッド ビュー) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.channelnames
helpviewer_keywords:
- Concurrency Visualizer, Channels (Threads View)
ms.assetid: 2f798c17-2363-42a4-be94-a5751d208eac
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 94ac6e9e85a2d7dd504b2d2bd83bd1bbdb265ea0
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56642847"
---
# <a name="channels-threads-view"></a>チャネル (スレッド ビュー)
コンカレンシー ビジュアライザーに、スレッド チャネル、ディスク チャネル、マーカー チャネル、GPU チャネルという 4 種類のチャネルが表示されます。

## <a name="thread-channels"></a>スレッド チャネル
 スレッド チャネルには、1 つのスレッドのスレッドの状態が色分けして表示されます。 チャネル名を一時停止すると、特定のスレッドの start 関数が表示されます。 コンカレンシー ビジュアライザーは、いくつかの種類のスレッドを検出します。 次の表は、最も一般的な種類を示しています。

|||
|-|-|
|メイン スレッド:|アプリで開始されたスレッド。|
|ワーカー スレッド|アプリケーションのメイン スレッドにより作成されたスレッド。|
|CLR ワーカー スレッド|共通言語ランタイム (CLR) によって作成されたワーカー スレッド。|
|デバッガー ヘルパー|Visual Studio デバッガーによって作成されたワーカー スレッド。|
|ConcRT スレッド|Microsoft のコンカレンシー ランタイムによって作成されたスレッド。|
|GDI スレッド|GDIPlus によって作成されたスレッド。|
|OLE/RPC スレッド|RPC ワーカー スレッドとして作成されたスレッド。|
|RPC スレッド|RPC スレッドとして作成されたスレッド。|
|WinSock スレッド|Winsock スレッドとして作成されたスレッド。|
|スレッド プール|CLR スレッド プールによって作成されたスレッド。|

## <a name="disk-channels"></a>ディスク チャネル
 ディスクのチャネルは、コンピューターの物理ドライブに対応します。 システム上の物理ドライブごとに読み取りおよび書き込み操作用の個別のチャネルがあるため、各ドライブには、2 つのチャネルがあります。 ディスク番号は、カーネルのデバイス名に対応します。 ディスク チャネルは、ディスクのアクティビティがあった場合にのみ表示されます。

## <a name="marker-channels"></a>マーカー チャネル
 マーカー チャネルは、アプリおよびそれが使用するライブラリによって生成されたイベントに対応します。 たとえば、タスク並列ライブラリ、並列パターン ライブラリ、および C++ AMP は、マーカーとして表示されているイベントを生成します。 各マーカー チャネルは、チャネルの説明の横に表示されるスレッド ID に関連付けられます。 ID は、イベントを生成したスレッドを識別します。 チャネルの説明には、イベントを生成した Event Tracing for Windows (ETW) プロバイダーの名前が含まれています。 チャネルが、[コンカレンシー ビジュアライザー SDK](../profiling/concurrency-visualizer-sdk.md) からのイベントを表示する場合、系列名も表示されます。

## <a name="gpu-channels"></a>GPU チャネル
 GPU チャネルは、システム上の DirectX 11 の活動に関する情報を表示します。  グラフィックス カードに関連付けられている各 DirectX エンジンに個別のチャネルがあります。  個々のセグメントは、DMA パケットの処理に費やした時間を表します。

## <a name="see-also"></a>関連項目
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)