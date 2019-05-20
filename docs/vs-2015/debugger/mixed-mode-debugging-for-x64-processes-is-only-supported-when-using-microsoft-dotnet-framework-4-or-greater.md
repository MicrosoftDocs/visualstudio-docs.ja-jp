---
title: 混合モード デバッグ プロセスが Microsoft.NET Framework 4 を使用する場合にのみサポートされている x64 より |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.error.interop_unsupported_x64
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: b7495655-54c0-4315-8422-43bf63b8c22e
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e974269cccb65db66ee59735f7acc5de494e2106
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697826"
---
# <a name="mixed-mode-debugging-for-x64-processes-is-only-supported-when-using-microsoftnet-framework-4-or-greater"></a>x64 プロセスの混合モード デバッグは、4 より前の Microsoft .NET Framework バージョンを使用している場合にはサポートされません。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

NET Framework のバージョン以前 4 よりはサポートされていません x64 の混合モード デバッグを処理します。 つまり、デバッグ中にマネージド コードからネイティブ コードにステップ インすることや、ネイティブ コードからマネージド コードにステップ インすることはできません。  
  
### <a name="workarounds"></a>問題回避  
  
- Microsoft .NET Framework 4 以降を使用するようにプロジェクトを更新する。  
  
     または  
  
     マネージド コードとネイティブ コードを個別のデバッガー セッション内でデバッグする。  
  
     または  
  
     次の手順に示すように、混合コードを 32 ビット プロセスとしてデバッグする。  
  
### <a name="to-change-the-platform-to-32-bit-visual-basic-or-c"></a>プラットフォームを 32 ビットに変更するには (Visual Basic または C#)  
  
1. **ソリューション エクスプローラー**で、プロジェクトを右クリックして、**[プロパティ]** をクリックします。  
  
2. プロパティ ページで、**[コンパイル]** タブまたは **[デバッグ]** タブをクリックします。  
  
3. **[プラットフォーム]** をクリックし、プラットフォームの一覧から [x86] を選択します。  
  
     Visual Basic コンパイラおよび C# コンパイラの既定では、どの CPU 上でも実行されるコードが生成されます。 64 ビット コンピューター上では、これらのバイナリは 64 ビット プロセスとして実行されます。 32 ビット プロセスとして実行するには、**[Any CPU]** でなく **[Win32]** を選択する必要があります。  
  
### <a name="to-change-the-platform-to-32-bit-cc"></a>プラットフォームを 32 ビットに変更するには (C/C++)  
  
1. **ソリューション エクスプローラー**で、プロジェクトを右クリックして、**[プロパティ]** をクリックします。  
  
2. プロパティ ページで **[プラットフォーム]** をクリックし、プラットフォームの一覧の [Win32] をクリックします。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 参照してください[SQL デバッグ セットアップ](https://msdn.microsoft.com/3db09e68-edcc-42de-9c22-4e97cfd55ab3)します。  
  
## <a name="see-also"></a>関連項目  
 [64 ビット アプリケーションをデバッグする](../debugger/debug-64-bit-applications.md)
