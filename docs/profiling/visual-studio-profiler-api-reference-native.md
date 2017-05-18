---
title: "Visual Studio プロファイラー API リファレンス (ネイティブ) | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- performance tools, API
- Profiler, API
ms.assetid: a0c3be92-c263-4678-9fb9-bafead3bd5f5
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: c9df048a49580f3526b48e29041ef3758722ed27
ms.openlocfilehash: 142df9fbf327ee8ebc39c3558ef1632a1bd23ae7
ms.contentlocale: ja-jp
ms.lasthandoff: 05/03/2017

---
# <a name="visual-studio-profiler-api-reference-native"></a>Visual Studio プロファイラー API リファレンス (ネイティブ)
Visual Studio プロファイラー API を使用すると、収集データの量をプログラムで制御したり、タイムスタンプとプロファイルの両方のマークをプロファイル時に挿入したりできます。 ネイティブ API を使用するには、VSPerf.h ヘッダー ファイルをインクルードし、VSPerf.lib をプロジェクトに追加する必要があります。  
  
> [!NOTE]
>  既定では、VSPerf.h と VSPerf.lib は PerfSDK という名前のフォルダーにあります。 たとえば、\<ドライブ>:\Program Files\Microsoft Visual Studio 14.0\Team Tools\Performance Tools\PerfSDK ディレクトリなどです。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [CommentMarkAtProfile](../profiling/commentmarkatprofile.md)  
  
 [CommentMarkProfile](../profiling/commentmarkprofile.md)  
  
 [MarkProfile](../profiling/markprofile.md)  
  
 [NameProfile](../profiling/nameprofile.md)  
  
 [ResumeProfile](../profiling/resumeprofile.md)  
  
 [StartProfile](../profiling/startprofile.md)  
  
 [StopProfile](../profiling/stopprofile.md)  
  
 [SuspendProfile](../profiling/suspendprofile.md)  
  
 [PROFILE_CURRENTID](../profiling/profile-currentid.md)  
  
## <a name="see-also"></a>関連項目  
 [プロファイリング ツールの API](../profiling/profiling-tools-apis.md)   
 [チュートリアル : プロファイラー API の使用](../profiling/walkthrough-using-profiler-apis.md)

