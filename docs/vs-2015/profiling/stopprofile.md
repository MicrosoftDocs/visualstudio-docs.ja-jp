---
title: StopProfile | Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- StopProfile
ms.assetid: be75b03c-7af5-4abe-a54a-6ee5479ad877
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 326ed9afa9d277babde5cda99ba5640f6d66bd98
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47547018"
---
# <a name="stopprofile"></a>StopProfile
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[StopProfile](https://docs.microsoft.com/visualstudio/profiling/stopprofile)します。  
  
`StopProfile` 関数は、指定されたプロファイル レベルのカウンターを 0 (オフ) に設定します。  
  
## <a name="syntax"></a>構文  
  
```  
PROFILE_COMMAND_STATUS PROFILERAPI StopProfile(  
                       PROFILE_CONTROL_LEVEL Level,   
                       unsigned int dwId);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `Level`  
  
 パフォーマンス データ収集を適用できるプロファイル レベルを示します。 次の **PROFILE_CONTROL_LEVEL** 列挙子を使用して、パフォーマンス データ収集を適用できる 3 つのレベルのいずれかを示すことができます。  
  
|列挙子|説明|  
|----------------|-----------------|  
|PROFILE_GLOBALLEVEL|グローバル レベル設定は、プロファイル実行のすべてのプロセスとスレッドに影響します。|  
|PROFILE_PROCESSLEVEL|プロセス レベル設定は、指定されたプロセスの一部であるスレッドすべてに影響します。|  
|PROFILE_THREADLEVEL|スレッド プロファイル レベル設定は、指定されたスレッドに影響します。|  
  
 `dwId`  
  
 システムによって生成される、プロセスまたはスレッドの ID。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 関数の成功または失敗は、**PROFILE_COMMAND_STATUS** 列挙型を使って表されます。 戻り値は次のいずれかになります。  
  
|列挙子|説明|  
|----------------|-----------------|  
|PROFILE_ERROR_ID_NOEXIST|プロファイル要素 ID が存在しません。|  
|PROFILE_ERROR_LEVEL_NOEXIST|指定されたプロファイル レベルが存在しません。|  
|PROFILE_ERROR_MODE_NEVER|関数が呼び出されたときに、プロファイル モードが NEVER に設定されました。|  
|PROFILE_ERROR_NOT_YET_IMPLEMENTED|プロファイル関数呼び出し、プロファイル レベル、または呼び出しとレベルの組み合わせがまだ実装されていません。|  
|PROFILE_OK|呼び出しに成功しました。|  
  
## <a name="remarks"></a>Remarks  
 StartProfile および StopProfile によって、プロファイル レベルの開始/停止状態を制御します。 開始/停止の既定値は 1 です。 初期値はレジストリで変更できます。 StartProfile を呼び出すたびに、開始/停止が 1 に設定され、StopProfile を呼び出すたびに 0 に設定されます。  
  
 開始/停止が 0 よりも大きい場合、そのレベルの開始/停止状態はオンになります。 開始/停止が 0 以下の場合、開始/停止状態はオフになります。  
  
 開始/停止状態と保留/再開状態の両方がオンの場合、そのレベルのプロファイル状態はオンです。 プロファイルの対象となるスレッドでは、グローバル、プロセス、およびスレッド レベル状態がオンである必要があります。  
  
## <a name="net-framework-equivalent"></a>同等の .NET Framework 関数  
 Microsoft.VisualStudio.Profiler.dll  
  
## <a name="function-information"></a>関数の情報  
 ヘッダー : VSPerf.h で宣言  
  
 インポート ライブラリ : VSPerf.lib  
  
## <a name="example"></a>例  
 StopProfile メソッドの例を以下に示します。 この例は、[PROFILE_CURRENTID](../profiling/profile-currentid.md) で識別される同じスレッドまたはプロセスに対して、StartProfile メソッドが呼び出されていることを前提としています。  
  
```  
void ExerciseStopProfile()  
{  
    // StartProfile and StopProfile control the   
    // Start/Stop state for the profiling level.   
    // The default initial value of Start/Stop is 1.   
    // The initial value can be changed in the registry.   
    // Each call to StartProfile sets Start/Stop to 1;   
    // each call to StopProfile sets it to 0.   
  
    // Variables used to print output.  
    HRESULT hResult;  
    TCHAR tchBuffer[256];  
  
    // Declare enumeration to hold result of call  
    // to StopProfile.  
    PROFILE_COMMAND_STATUS profileResult;  
  
    profileResult = StopProfile(  
        PROFILE_THREADLEVEL,  
        PROFILE_CURRENTID);  
  
    // Format and print result.  
    LPCTSTR pszFormat = TEXT("%s %d.\0");  
    TCHAR* pszTxt = TEXT("StopProfile returned");  
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,   
        pszTxt, profileResult);  
  
#ifdef DEBUG  
    OutputDebugString(tchBuffer);  
#endif  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio プロファイラー API リファレンス (ネイティブ)](../profiling/visual-studio-profiler-api-reference-native.md)



