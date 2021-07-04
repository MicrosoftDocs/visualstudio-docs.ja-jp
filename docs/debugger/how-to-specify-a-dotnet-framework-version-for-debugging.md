---
title: デバッグ用の .NET Framework のバージョンを指定する | Microsoft Docs
description: デバッグ用に古い .NET Framework のバージョンを指定します。 Visual Studio デバッガーでは、.NET Framework の現在のバージョンだけでなく、古いバージョンのデバッグもサポートされています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- .NET Framework, specifying version for debugging
- debugging [Visual Studio], specifying .NET Framework version
ms.assetid: 7a4893ba-4620-4774-893f-378d4ca28893
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 83b30067530b9a48769879f3a222fee2afa725c0
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384669"
---
# <a name="specify-an-older-net-framework-version-for-debugging-c-visual-basic-f"></a>デバッグ用に古い .NET Framework バージョンを指定する (C#、Visual Basic、F#)

Visual Studio デバッガーでは、Microsoft .NET Framework の現在のバージョンだけでなく、古いバージョンのデバッグもサポートされています。 Visual Studio からアプリケーションを起動すると、デバッグするアプリケーション用の適切なバージョンの .NET Framework がデバッガーによって常に識別されます。 ただし、アプリケーションが既に実行されていて、 **[アタッチ先]** を使用することでデバッグを開始した場合、デバッガーで .NET Framework の古いバージョンが常に識別できるとは限りません。 この場合、次のようなエラー メッセージが出力されます。

``` cmd
The debugger has made an incorrect assumption about the .NET Framework version your application is going to use.
```

このエラーはめったに発生しませんが、発生した場合は、レジストリ キーを設定して、どのバージョンを使用するかをデバッガーに指示できます。

### <a name="to-specify-a-net-framework-version-for-debugging"></a>デバッグで .NET Framework のバージョンを指定するには

1. コンピューターにインストールされている .NET Framework のバージョンを確認するには、Windows\Microsoft.NET\Framework ディレクトリを探します。 バージョン番号は次のようになります。

    `V1.1.4322`

    正しいバージョン番号を確認し、メモしておきます。

2. **レジストリ エディター** (regedit) を起動します。

3. **レジストリ エディター** で、[HKEY_LOCAL_MACHINE] フォルダーを開きます。

4. 次に移動します。HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\10.0\AD7Metrics\Engine\\{449EC4CC-30D2-4032-9256-EE18EB41B62B}

    このキーが存在しない場合、HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\10.0\AD7Metrics\Engine を右クリックし、 **[新しいキー]** をクリックします。 新しいキーに `{449EC4CC-30D2-4032-9256-EE18EB41B62B}` という名前を付けます。

5. {449EC4CC-30D2-4032-9256-EE18EB41B62B} に移動し、 **[名前]** 列を確認して、CLRVersionForDebugging キーを探します。

   1. このキーが存在しない場合、{449EC4CC-30D2-4032-9256-EE18EB41B62B} を右クリックし、 **[新規] - [文字列値]** をクリックします。 次に、新しい文字列値を右クリックし、 **[名前の変更]** をクリックし、「`CLRVersionForDebugging`」と入力します。

6. **[CLRVersionForDebugging]** をダブルクリックします。

7. **[文字列の編集]** ボックスの **[値]** ボックスに、.NET Framework のバージョン番号を入力します。 次に例を示します。V1.1.4322

8. **[OK]** をクリックします。

9. **レジストリ エディター** を閉じます。

     それでもデバッグの開始時にエラー メッセージが表示される場合は、レジストリに正しいバージョン番号が入力されていることを確認します。 また、Visual Studio でサポートされている .NET Framework のバージョンを使用していることを確認します。 デバッガーは、現在のバージョンおよび以前のバージョンの .NET Framework と互換性がありますが、将来のバージョンとの上位互換性はない可能性があります。

## <a name="see-also"></a>関連項目
- [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)