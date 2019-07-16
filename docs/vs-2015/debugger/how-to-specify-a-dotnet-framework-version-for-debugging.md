---
title: '方法: デバッグ用の .NET Framework のバージョンの指定 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- .NET Framework, specifying version for debugging
- debugging [Visual Studio], specifying .NET Framework version
ms.assetid: 7a4893ba-4620-4774-893f-378d4ca28893
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4c785c419ead31ad90e2b20ae7f48af778598bb6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68176563"
---
# <a name="how-to-specify-a-net-framework-version-for-debugging"></a>方法: デバッグ用の .NET Framework のバージョンを指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] デバッガーでは、Microsoft [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] の現在のバージョンだけでなく、古いバージョンのデバッグもサポートしています。 Visual Studio からアプリケーションを起動すると、デバッグしているアプリケーションの [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] バージョンは正しく識別されます。 使用すると、アプリケーションが既に実行されている**にアタッチ**、デバッガーは常にできないことがありますの以前のバージョンを識別するために、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]します。 この場合、次のようなエラー メッセージが出力されます。  
  
 "アプリケーションが使用しようとしている Microsoft [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] のバージョンに関してデバッガーが不適切な想定を行っています。"  
  
 このような場合はまれですが、使用するデバッガーのバージョンを指定するには、レジストリ キーを設定します。  
  
### <a name="to-specify-a-net-framework-version-for-debugging"></a>デバッグで .NET Framework のバージョンを指定するには  
  
1. コンピューターにインストールされている .NET Framework のバージョンを確認するには、Windows\Microsoft.NET\Framework ディレクトリを探します。 バージョン番号は次のようになります。  
  
     `V1.1.4322`  
  
     正しいバージョン番号を確認し、メモしておきます。  
  
2. **レジストリ エディター** (regedit) を起動します。  
  
3. **レジストリ エディター**で、[HKEY_LOCAL_MACHINE] フォルダーを開きます。  
  
4. 次に移動します。HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\10.0\AD7Metrics\Engine\\{449ec4cc-30d2-4032-9256-ee18eb41b62b}  
  
     このキーが存在しない場合、HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\10.0\AD7Metrics\Engine を右クリックし、 **[新しいキー]** をクリックします。 新しいキーの名前`{449EC4CC-30D2-4032-9256-EE18EB41B62B}`します。  
  
5. {449EC4CC-30D2-4032-9256-EE18EB41B62B} に移動し、 **[名前]** 列を確認して、CLRVersionForDebugging キーを探します。  
  
    1. このキーが存在しない場合、{449EC4CC-30D2-4032-9256-EE18EB41B62B} を右クリックし、 **[新規] - [文字列値]** をクリックします。 新しい文字列値を右クリックし、をクリックして**の名前を変更**、および種類`CLRVersionForDebugging`します。  
  
6. **[CLRVersionForDebugging]** をダブルクリックします。  
  
7. **[文字列の編集]** ボックスの **[値]** ボックスに、.NET Framework のバージョン番号を入力します。 例えば:V1.1.4322  
  
8. **[OK]** をクリックします。  
  
9. **レジストリ エディター**を閉じます。  
  
     それでもデバッグの開始時にエラー メッセージが表示される場合は、レジストリに正しいバージョン番号が入力されていることを確認します。 また、Visual Studio でサポートされている [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] のバージョンを使用していることを確認します。 デバッガーは、現在のバージョンおよび以前のバージョンの .NET Framework と互換性がありますが、将来のバージョンとの上位互換性はない可能性があります。  
  
## <a name="see-also"></a>関連項目  
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)
