---
title: '方法 : 追加のインストルメンテーション オプションを指定する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.property.advanced
helpviewer_keywords:
- instrumentation, options
- profiling tools, session options
- performance sessions, options
ms.assetid: 639afe26-8335-4bd4-8aa5-f2c607b81f07
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4efa493afa7257d4460fd106a0a9685930ca3e59
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54803044"
---
# <a name="how-to-specify-additional-instrumentation-options"></a>方法 : 追加のインストルメンテーション オプションを指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

バイナリをインストルメントする方法には、[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 統合開発環境 (IDE: Integrated Development Environment) から行う方法と、コマンド ライン ツールを使用する方法があります。 IDE 内からバイナリをインストルメント化する場合は、[VSInstr](../profiling/vsinstr.md) ツールに追加のインストルメンテーション オプションを指定することで、インストルメンテーション中に収集されるデータの量を制御できます。 これらのオプションは、セッション レベルまたはターゲット レベルで使用できます。 たとえば、インストルメンテーション プロセスにおいて特定の関数を含めたり除外したりするには、ターゲット レベルで追加のインストルメンテーション オプションを使用します。  
  
 **必要条件**  
  
-   [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、 [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]、 [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
> [!IMPORTANT]
>  プローブを挿入すると、必ず元のプログラムの動作がわずかに変化します。 この変化により、分析時にオーバーヘッドが発生します。 このオーバーヘッドの概算値を差し引いたとしても、マルチスレッド アプリケーションにおいてタイミング上の影響がわずかに残ります。 [VSInstr](../profiling/vsinstr.md) ツール オプションを使用すると、プロファイリング中のデータ収集を制御できます。  
  
### <a name="to-specify-additional-instrumentation-option"></a>追加のインストルメンテーション オプションを指定するには  
  
1.  **パフォーマンス エクスプローラー**で、**パフォーマンス セッション**を選択して右クリックし、**[プロパティ]** を選択します。  
  
2.  **[プロパティ ページ]** で **[詳細]** プロパティをクリックします。  
  
3.  **[追加インストルメンテーション オプション]** ボックスにオプションを入力します。  
  
     たとえば、プロファイル レベルを指定するには「/CONTROL:THREAD」と入力します。 オプションの一覧については「[VSInstr](../profiling/vsinstr.md)」をご覧ください。  
  
4.  **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)   
 [コマンドラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)
