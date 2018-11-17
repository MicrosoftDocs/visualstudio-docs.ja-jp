---
title: 'DA0506: プロセスに割り当てられた最大プライベート バイト数がプロファイリングされています | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.performance.rules.DA0506
- vs.performance.DA0506
- vs.performance.506
ms.assetid: e9c43554-9a85-4d98-9fa4-3b19986e7b62
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bdd7d63ad7dd0261394d3333cdd35ec5f5a330f1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810391"
---
# <a name="da0506-maximum-private-bytes-allocated-for-the-process-being-profiled"></a>DA0506: プロセスに割り当てられた最大プライベート バイト数がプロファイリングされています
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

規則 Id |DA 0506 |  
|カテゴリ |リソースの監視 |  
|プロファイル方法 |すべて |  
|メッセージ |この情報がについてのみ収集されます。 Process Private Bytes カウンターは、プロファイリングを行っているプロセスによって割り当てられた仮想メモリを測定します。 報告される値は、全測定期間を通じて観察された最大値 |。  
|規則の種類 |情報 |  
  
 サンプリング、.NET メモリ、またはリソース競合メソッドを使用してプロファイリングを行うときは、この規則を呼び出すためのサンプルを少なくとも 10 個収集する必要があります。  
  
## <a name="rule-description"></a>規則の説明  
 このメッセージにより、プロセスによって割り当てられた現在の仮想メモリの最大容量がバイト単位で報告されます (プライベート バイト)。 プライベート バイトは、プロセス内部で実行中のスレッドからのみアクセスできるプロセスによって割り当てられた仮想メモリの位置を表します。  
  
 32 ビット コンピューター上で実行されている 32 ビット プロセスの場合、プロセスのアドレス空間のプライベート領域の上限は 2 GB です。 [/3 GB](http://go.microsoft.com/fwlink/?LinkId=177831) Boot.ini スイッチを使用して、32 ビット プロセスは、最大 3 GB の仮想メモリを取得できます。 64 ビット コンピューター上で実行されている 32 ビット プロセスの場合、最大 4 GB のプライベート仮想メモリを取得できます。  
  
 64 ビット コンピューター上で実行されている 64 ビット プロセスの場合、最大 8 TB のプライベート仮想メモリを取得できます。  
  
 プロファイリング中のプロセスがアクティブな状態にあるすべての測定間隔を通じて、最も大きな値がこのメッセージによって報告されます。  
  
 プロセス アドレス空間の詳細については、Windows のメモリ管理のドキュメントの「[Virtual Address Space](http://go.microsoft.com/fwlink/?LinkId=177832)」 (仮想アドレス空間) を参照してください。  
  
## <a name="how-to-use-rule-data"></a>規則データの使用方法  
 報告された値を使用して、特定のプログラムの異なるバージョンやビルドを比較したり、さまざまなプロファイリング シナリオにおけるアプリケーションのパフォーマンスを確認したりします。  
  
 プロセスのプライベート バイトの最大値が、プロセスのアドレス空間が占めることができる設計上の上限に近づくと、メモリ不足による例外が発生する可能性があります。 詳細については MSDN マガジンの「[Investigating Memory Issues](http://go.microsoft.com/fwlink/?LinkID=177833)」 (メモリの問題を調査する) を参照してください。



