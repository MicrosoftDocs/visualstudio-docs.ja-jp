---
title: 従来の言語サービスの移行 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, migrating
ms.assetid: e0f666a0-92a7-4f9c-ba79-d05b13fb7f11
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2df11ccfc2057da37094c632c10fc9c1a936cf43
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56612437"
---
# <a name="migrating-a-legacy-language-service"></a>従来の言語サービスの移行
以降のバージョンの Visual Studio に従来の言語サービスを移行するには、プロジェクトを更新して、source.extension.vsixmanifest ファイルをプロジェクトに追加します。 言語サービス自体は引き続き機能と同様に、Visual Studio エディターで適応させるのでします。

 従来の言語サービスは、VSPackage の一部として実装されますが、言語サービスの機能を実装する新しい方法は MEF 拡張機能を使用します。 言語サービスを実装する新しい方法の詳細についてを参照してください。[エディターと言語サービス拡張](../../extensibility/editor-and-language-service-extensions.md)します。

> [!NOTE]
>  新しいエディターの API をできるだけ早く使用を開始することをお勧めします。 言語サービスのパフォーマンスを向上させる、エディターの新機能を活用することができます。

## <a name="migrating-a-visual-studio-2008-language-service-solution-to-a-later-version"></a>以降のバージョンに、Visual Studio 2008 の言語サービス ソリューションを移行します。
 次の手順では、RegExLanguageService という名前の Visual Studio 2008 サンプルを適合させる方法を示します。 Visual Studio 2008 SDK のインストールでこのサンプルを見つけることができます、 *Visual Studio SDK インストール パス*\VisualStudioIntegration\Samples\IDE\CSharp\Example.RegExLanguageService\ フォルダー。

> [!IMPORTANT]
>  明示的に設定する必要がある、言語サービスが色を定義していない場合<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute.RequestStockColors%2A>に`true`を VSPackage に。

```
[Microsoft.VisualStudio.Shell.ProvideLanguageService(typeof(YourLanguageService), YourLanguageServiceName, 0, RequestStockColors = true)]
```

#### <a name="to-migrate-a-visual-studio-2008-language-service-to-a-later-version"></a>以降のバージョンの Visual Studio 2008 の言語サービスに移行するには

1.  Visual Studio と Visual Studio SDK の新しいバージョンをインストールします。 SDK をインストールする方法の詳細については、[Visual Studio SDK をインストールする](../../extensibility/installing-the-visual-studio-sdk.md)を参照してください。

2.  (Visual Studio に読み込んでなし、RegExLangServ.csproj ファイルを編集します。

     `Import` Microsoft.VsSDK.targets ファイルを参照するノードは、値を次のテキストに置き換えます。

    ```
    $(MSBuildExtensionsPath)\Microsoft\VisualStudio\v14.0\VSSDK\Microsoft.VsSDK.targets
    ```

3.  ファイルを保存して、閉じます。

4.  RegExLangServ.sln ソリューションを開きます。

5.  **一方向のアップグレード**ウィンドウが表示されます。 **[OK]** をクリックします。

6.  プロジェクトのプロパティを更新します。 開く、**プロジェクト プロパティ**ウィンドウでプロジェクト ノードを選択して、**ソリューション エクスプ ローラー**、右クリックし、および選択**プロパティ**します。

    -   **アプリケーション** タブで、変更**ターゲット フレームワーク**に**4.6.1**します。

    -   **デバッグ** タブで、**外部プログラムの開始**ボックスに「  **\<Visual Studio インストール パス > \Common7\IDE\devenv.exe。** します。

         **コマンドライン引数**ボックスに、入力/**/rootsuffix Exp**します。

7.  次の参照を更新します。

    -   Microsoft.VisualStudio.Shell.9.0.dll への参照を削除し、Microsoft.VisualStudio.Shell.14.0.dll および Microsoft.VisualStudio.Shell.Immutable.11.0.dll への参照を追加します。

    -   Microsoft.VisualStudio.Package.LanguageService.9.0.dll への参照を削除し、Microsoft.VisualStudio.Package.LanguageService.14.0.dll への参照を追加します。

    -   Microsoft.VisualStudio.Shell.Interop.10.0.dll への参照を追加します。

8.  VsPkg.cs ファイルを開きの値を変更、`DefaultRegistryRoot`属性を

    ```
    "Software\\Microsoft\\VisualStudio\\14.0Exp"
    ```

9. 元のサンプルでは、VsPkg.cs し、次の属性を追加する必要があります、その言語サービスは登録されません。

    ```
    [ProvideLanguageService(typeof(RegularExpressionLanguageService), "RegularExpressionLanguage", 0, RequestStockColors=true)]
    ```

10. Source.extension.vsixmanifest ファイルを追加する必要があります。

    -   既存の拡張機能から、プロジェクト ディレクトリにこのファイルをコピーします。 (このファイルを取得する方法の 1 つは、VSIX プロジェクトを作成することです。 (**ファイル**、 をクリック**新規**、 をクリックし、**プロジェクト**。 Visual Basic または c# のクリック**拡張**を選択し、 **VSIX プロジェクト**)。

    -   ファイルをプロジェクトに追加します。

    -   ファイルの**プロパティ**設定**ビルド アクション**に**None**します。

    -   ファイルを開く、 **VSIX マニフェスト エディター**します。

    -   次のフィールドを変更します。

    -   **ID**:RegExLangServ

    -   **製品名**:RegExLangServ

    -   **説明**:正規表現の言語サービス。

    -   [**資産**、] をクリックして**新規**を選択します、**型**に**Microsoft.VisualStudio.VsPackage**、設定、**ソース**に**現在のソリューションでプロジェクトを**、し、設定、**プロジェクト**に**RegExLangServ**します。

    -   ファイルを保存して閉じます。

11. ソリューションをビルドします。 ビルドされたファイルに配置されます **%USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0Exp\Extensions\MSIT\ RegExLangServ\\**します。

12. デバッグを開始します。 Visual Studio の 2 番目のインスタンスが開かれます。

## <a name="see-also"></a>関連項目
- [従来の言語サービスの機能拡張](../../extensibility/internals/legacy-language-service-extensibility.md)