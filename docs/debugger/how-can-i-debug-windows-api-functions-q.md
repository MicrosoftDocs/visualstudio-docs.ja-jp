---
title: Windows API 関数のデバッグ |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.api
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], Windows API functions
- NT symbols and debugging Windows API functions
- Windows API functions, debugging
- Windows API, debugging API functions
- APIs, debugging
ms.assetid: 7c126f57-62ab-4d94-9805-632d696ba1f0
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9d10c4804d4d53c22281c11d8afc464cf2ac3732
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53861515"
---
# <a name="how-can-i-debug-windows-api-functions"></a>Windows API 関数をデバッグするには
NT シンボルを読み込んだ状態で Windows API 関数をデバッグするには、次の手順を実行する必要があります。  
  
### <a name="to-set-a-breakpoint-on-a-windows-api-function-with-nt-symbols-loaded"></a>NT シンボルを読み込んだ状態で Windows API 関数にブレークポイントを設定するには  
  
-   関数の名前と、関数が存在する DLL の名前を入力します。 32 ビット コードでは、関数名の装飾形式を使用します。 たとえば、**MessageBeep** にブレークポイントを設定するには、次のように入力します。  
  
    ```cpp
    {,,USER32.DLL}_MessageBeep@4  
    ```  
  
     装飾名を取得するには、次を参照してください。[装飾名の確認](https://msdn.microsoft.com/library/f79e2717-a4db-4d12-a689-69830cce2be0)します。  
  
## <a name="see-also"></a>「  
 [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)   
 [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
