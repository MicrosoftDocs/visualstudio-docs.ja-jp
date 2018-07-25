---
title: NameProfile | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- NameProfile
- NameProfileA
ms.assetid: 1bb05441-c4ff-4323-9fef-f3924fba4430
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3f52b647cb6d110d111666df172d7243b0fd8ea4
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2018
ms.locfileid: "35256137"
---
# <a name="nameprofile"></a>NameProfile
`NameProfile` 関数は、指定したプロセスまたはスレッドに文字列を割り当てます。  
  
 NameProfile API は、インストルメンテーション プロファイリングでのみ使用できます。 NameProfile API は、サンプリング プロファイリングではサポートされません。  
  
## <a name="syntax"></a>構文  
  
```cpp  
PROFILE_COMMAND_STATUS PROFILERAPI NameProfile(  
                                   LPCTSTR pszName,   
                                   PROFILE_CONTROL_LEVEL Level,  
                                   unsigned int dwId);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszName`  
  
 プロファイル要素の名前。 次の場合、名前は無効です (NameProfileA は NAME_ERROR_INVALID_NAME を返します)。  
  
-   NameProfileA に渡されたポインターが NULL 値である。  
  
-   pszName の文字列データの先頭が数値である。  
  
-   pszName の文字列データに空白が含まれる。  
  
-   pszName の文字列データに、,;.`~!@#$%^&*()=[]{}&#124;\\?/<> 文字のいずれかが含まれる。  
  
 `Level`  
  
 パフォーマンス データ収集を適用できるプロファイル レベルを示します。 次の **PROFILE_CONTROL_LEVEL** 値を使用して、パフォーマンス データ収集を適用できる 3 つのレベルのいずれかを指定できます。  
  
|列挙子|説明|  
|----------------|-----------------|  
|PROFILE_GLOBALLEVEL|グローバル レベル設定は、プロファイル実行のすべてのプロセスとスレッドに影響します。|  
|PROFILE_PROCESSLEVEL|プロセス レベル設定は、指定されたプロセスの一部であるスレッドすべてに影響します。|  
|PROFILE_THREADLEVEL|スレッド プロファイル レベル設定は、指定されたスレッドに影響します。|  
  
 `dwId`  
  
 プロファイル レベル ID。 システムにより生成されたプロセス ID またはスレッド ID を使用します。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 関数の成功または失敗は、**PROFILE_COMMAND_STATUS** 列挙型を使って表されます。 戻り値は次のいずれかになります。  
  
|列挙子|説明|  
|----------------|-----------------|  
|NAME_ERROR_ID_NOEXIST|指定されたプロファイル要素が存在しません。|  
|NAME_ERROR_INVALID_NAME|名前が無効です。|  
|NAME_ERROR_LEVEL_NOEXIST|指定されたプロファイル レベルが存在しません。|  
|NAME_ERROR_NO_SUPPORT|指定された操作がサポートされていません。|  
|NAME_ERROR_OUTOFMEMORY|メモリ不足のため、このイベントを記録できません。|  
|NAME_ERROR_REDEFINITION|プロファイル要素には既に名前が割り当てられています。 この関数の名前は無視されます。|  
|NAME_ERROR_TEXTTRUNCATED|名前のテキストが null 文字を含めて 32 文字を超えていたため、切り詰められました。|  
|NAME_OK|名前は正常に登録されました。|  
  
## <a name="remarks"></a>コメント  
 各プロセスまたはスレッドには、名前を 1 つのみ割り当てることができます。 プロファイル要素に名前を付けた後で、その要素の NameProfile を呼び出しても無視されます。  
  
 異なるスレッドまたはプロセスに同じ名前が指定されている場合、その名前を持つそのレベルのすべての要素のデータがレポートに含まれます。  
  
 現在のもの以外のプロセスまたはスレッドを指定した場合、それが初期化され、実行が開始されていることを確認した後で名前を付ける必要があります。 それ以外の場合、NameProfile メソッドは失敗します。  
  
> [!IMPORTANT]
>  CreateProcess() API および CreateThread() API 関数は、スレッドまたはプロセスが初期化される前に値を返す場合があります。  
  
## <a name="net-framework-equivalent"></a>同等の .NET Framework 関数  
 *Microsoft.VisualStudio.Profiler.dll*  
  
## <a name="function-information"></a>関数の情報  
  
|||  
|-|-|  
|**Header**|*VSPerf.h* をインクルードします。|  
|**Library**|*VSPerf.lib* を使用します。|  
|**Unicode**|`NameProfileW` (Unicode) および `NameProfileA` (ANSI) として実装します。|  
  
## <a name="example"></a>例  
 次のコードは、NameProfile 関数の呼び出しの例です。 この例では、コードで ANSI 対応関数を呼び出すかどうかを判断するために、Win32 文字列マクロおよび ANSI のコンパイラ設定が使用されていることを前提としています。  
  
```cpp  
void ExerciseNameProfile()  
{  
    // Variables used to print output.  
    HRESULT hResult;  
    TCHAR tchBuffer[256];  
  
    // Create and initialize variables to pass to   
    // ExerciseNameProfile.  The value of this   
    // parameter is based on the needs of the code;  
    // and for the sake of simplicity in this example,   
    // the variable is assigned an arbitrary value.  
    TCHAR * profileName = TEXT("ExerciseNameProfile");  
  
    // Declare enumeration to hold result of call to   
    // ExerciseNameProfle.  
    PROFILE_COMMAND_STATUS nameResult;  
  
    nameResult =  NameProfile(  
        profileName,  
        PROFILE_GLOBALLEVEL,  
        PROFILE_CURRENTID);  
  
    // Format and print result.  
    LPCTSTR pszFormat = TEXT("%s %d.\0");  
    TCHAR* pszTxt = TEXT("NameProfile returned");  
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,   
        pszTxt, nameResult);  
  
#ifdef DEBUG  
    OutputDebugString(tchBuffer);  
#endif  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio プロファイラー API リファレンス (ネイティブ)](../profiling/visual-studio-profiler-api-reference-native.md)