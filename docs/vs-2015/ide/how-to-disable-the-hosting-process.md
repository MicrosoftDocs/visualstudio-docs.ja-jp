---
title: '方法 : ホスト プロセスを無効にする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- hosting process, disabling
- vshost.exe, disabling the hosting process
ms.assetid: 9157488d-737f-454b-8d8d-36f99de38bb0
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 0266e14b3a03e6d8225e7ec9283fe727a9502e53
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54785882"
---
# <a name="how-to-disable-the-hosting-process"></a>方法 : ホスト プロセスを無効にする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ホスト プロセスが有効になっていると、特定の API の呼び出しに影響する場合があります。 影響がある場合は、正しい結果が返るようにホスト プロセスを無効にする必要があります。  
  
### <a name="to-disable-the-hosting-process"></a>ホスト プロセスを無効にするには  
  
1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で、実行可能なプロジェクトを開きます。 実行可能ファイルを生成しないプロジェクト (クラス ライブラリやサービス プロジェクトなど) には、このオプションがありません。  
  
2. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
3. **[デバッグ]** タブをクリックします。  
  
4. **[Visual Studio ホスティング プロセスを有効にする]** チェック ボックスをオフにします。  
  
   ホスト プロセスが無効になると、一部のデバッグ機能が使用できなくなったり、パフォーマンスが低下したりします。 詳しくは、「[プロセスのデバッグとホスト](../debugger/debugging-and-the-hosting-process.md)」をご覧ください。  
  
   一般的に、ホスト プロセスが無効になると、次のことが起こります。  
  
-   [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] アプリケーションのデバッグが始まるまでの時間が長くなる。  
  
-   デザイン時の式評価が使用できなくなる。  
  
-   部分信頼デバッグが使用できなくなる。  
  
## <a name="see-also"></a>関連項目  
 [プロセスのデバッグとホスト](../debugger/debugging-and-the-hosting-process.md)   
 [ホスト プロセス (vshost.exe)](../ide/hosting-process-vshost-exe.md)   
 [アプリケーション開発時のビルド](http://msdn.microsoft.com/c9497d62-3b7b-4449-88e8-cf27acc9efe6)
