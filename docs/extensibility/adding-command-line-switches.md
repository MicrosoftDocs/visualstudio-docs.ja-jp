---
title: コマンドライン スイッチの追加 | Microsoft Docs
description: devenv.exe コマンドの実行時に VSPackage に適用されるコマンドライン スイッチを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- command-line switches, adding
- command-line switches, retrieving
- IVsAppCommandLine::GetOption method
- command line, switches
ms.assetid: 8bbbd87e-76fe-4fb5-8ef9-65f5e31967cf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 826029154763a98279b5e5446317802531b08bfe
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097566"
---
# <a name="add-command-line-switches"></a>コマンドライン スイッチを追加する
*devenv.exe* の実行時に VSPackage に適用されるコマンドライン スイッチを追加することができます。 <xref:Microsoft.VisualStudio.Shell.ProvideAppCommandLineAttribute> を使用して、スイッチの名前とそのプロパティを宣言します。 この例では、**AddCommandSwitchPackage** という名前の VSPackage のサブクラスに、引数なしで、MySwitch スイッチが追加され、VSPackage が自動的に読み込まれます。

```csharp
[ProvideAppCommandLine("MySwitch", typeof(AddCommandSwitchPackage), Arguments = "0", DemandLoad = 1)]
```

 名前付きパラメーターについては、次の説明を参照してください。

|名前|説明|
|-|-|
| 引数 | スイッチの引数の数。 "*" または引数の一覧を指定できます。 |
| DemandLoad | これを 1 に設定すると、VSPackage は自動的に読み込まれます。それ以外の場合は 0 に設定します。 |
| HelpString | **devenv /?** で表示するヘルプ文字列または文字列のリソース ID。 |
| 名前 | スイッチ。 |
| PackageGuid | パッケージの GUID。 |

 通常、引数の最初の値は 0 または 1 です。 '*' という特別な値を使用すると、コマンド ラインの残りの部分全体が引数であることを示すことができます。 これは、ユーザーがデバッガー コマンド文字列を渡す必要があるデバッグ シナリオで役立ちます。

 DemandLoad の値は `true` (1) または `false` (0) のいずれかであり、VSPackage を自動的に読み込む必要があるかどうかを示します。

 HelpString の値は、**devenv /?** で表示される文字列のリソース ID です。 ヘルプの表示。 この値は "#nnn" (nnn は整数) の形式にする必要があります。 リソース ファイルの文字列値は、改行文字で終わる必要があります。

 Name の値は、スイッチの名前です。

 PackageGuid の値は、このスイッチを実装するパッケージの GUID です。 IDE では、この GUID を使用して、コマンドライン スイッチが適用されるレジストリ内の VSPackage が検索されます。

## <a name="retrieve-command-line-switches"></a>コマンドライン スイッチを取得する
 パッケージが読み込まれたら、次の手順を実行してコマンドライン スイッチを取得できます。

1. VSPackage の <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 実装で、<xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine> に対して `QueryService` を呼び出して、<xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine> インターフェイスを取得します。

2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine.GetOption%2A> を呼び出して、ユーザーが入力したコマンドライン スイッチを取得します。

   次のコードは、MySwitch コマンドライン スイッチがユーザーによって入力されたかどうかを調べる方法を示しています。

```csharp
IVsAppCommandLine cmdline = (IVsAppCommandLine)GetService(typeof(SVsAppCommandLine));

int isPresent = 0;
string optionValue = "";

cmdline.GetOption("MySwitch", out isPresent, out optionValue);
```

 パッケージが読み込まれるたびに、コマンドライン スイッチを確認する必要があります。

## <a name="see-also"></a>参照
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- [Devenv コマンドライン スイッチ](../ide/reference/devenv-command-line-switches.md)
- [CreatePkgDef ユーティリティ](../extensibility/internals/createpkgdef-utility.md)
- [.Pkgdef ファイル](https://devblogs.microsoft.com/visualstudio/whats-a-pkgdef-and-why/)
