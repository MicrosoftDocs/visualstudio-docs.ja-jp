---
title: StartProfile | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- StartProfile
ms.assetid: 1761311d-c9d5-48f5-b1f8-b3605829940a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4e134db79df1457b3308fc86b2fbe2b133d8ce86
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/19/2018
---
# <a name="startprofile"></a>StartProfile
`StartProfile` 関数は、指定されたプロファイル レベルのカウンターを 1 (オン) に設定します。  
  
## <a name="syntax"></a>構文  
  
```  
PROFILE_COMMAND_STATUS PROFILERAPI StartProfile(  
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
  
## <a name="remarks"></a>コメント  
 StartProfile および StopProfile によって、プロファイル レベルの開始/停止状態を制御します。 開始/停止の既定値は 1 です。 初期値はレジストリで変更できます。 StartProfile を呼び出すたびに、開始/停止が 1 に設定され、StopProfile を呼び出すたびに 0 に設定されます。  
  
 開始/停止が 0 よりも大きい場合、そのレベルの開始/停止状態はオンになります。 開始/停止が 0 以下の場合、開始/停止状態はオフになります。  
  
 開始/停止状態と保留/再開状態の両方がオンの場合、そのレベルのプロファイル状態はオンです。 プロファイルの対象となるスレッドでは、グローバル、プロセス、およびスレッド レベル状態がオンである必要があります。  
  
## <a name="net-framework-equivalent"></a>同等の .NET Framework 関数  
 Microsoft.VisualStudio.Profiler.dll  
  
## <a name="function-information"></a>関数の情報  
 ヘッダー : VSPerf.h で宣言  
  
 インポート ライブラリ : VSPerf.lib  
  
## <a name="example"></a>例  
 StartProfile 関数の呼び出し例を以下に示します。  
  
```  
void ExerciseStartProfile()  
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
  
    // Declare enumeration to hold return value of   
    // the call to StartProfile.  
    PROFILE_COMMAND_STATUS profileResult;  
  
    profileResult = StartProfile(  
        PROFILE_THREADLEVEL,  
        PROFILE_CURRENTID);  
  
    // Format and print result.  
    LPCTSTR pszFormat = TEXT("%s %d.\0");  
    TCHAR* pszTxt = TEXT("StartProfile returned");  
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,   
        pszTxt, profileResult);  
  
#ifdef DEBUG  
    OutputDebugString(tchBuffer);  
#endif  
}  
```  
  
## <a name="see-also"></a>参照  
 [Visual Studio プロファイラー API リファレンス (ネイティブ)](../profiling/visual-studio-profiler-api-reference-native.md)