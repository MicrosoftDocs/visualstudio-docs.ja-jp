---
title: 従来の言語サービスの移行 | Microsoft Docs
description: プロジェクトを更新し、source.extension.vsixmanifest ファイルを追加することで、言語サービスを最新バージョンの Visual Studio に更新する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, migrating
ms.assetid: e0f666a0-92a7-4f9c-ba79-d05b13fb7f11
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: afe98f2d96618999aa02dd01f03f55395af46e19
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063267"
---
# <a name="migrating-a-legacy-language-service"></a>従来の言語サービスの移行
プロジェクトを更新し、source.extension.vsixmanifest ファイルをプロジェクトに追加することで、従来の言語サービスを新しいバージョンの Visual Studio に移行することができます。 言語サービス自体は引き続き以前と同じように機能します。これは、Visual Studio エディターが適応するためです。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 言語サービスの新しい実装方法の詳細については、「[エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="migrating-a-visual-studio-2008-language-service-solution-to-a-later-version"></a>Visual Studio 2008 言語サービス ソリューションの新しいバージョンへの移行
 次の手順は、RegExLanguageService という名前の Visual Studio 2008 サンプルを適応させる方法を示しています。 このサンプルは、Visual Studio 2008 SDK インストールの "*Visual Studio SDK インストール パス*"\VisualStudioIntegration\Samples\IDE\CSharp\Example.RegExLanguageService\ フォルダーにあります。

> [!IMPORTANT]
> 言語サービスに色が定義されていない場合は、VSPackage で <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute.RequestStockColors%2A> を `true` に明示的に設定する必要があります。

```
[Microsoft.VisualStudio.Shell.ProvideLanguageService(typeof(YourLanguageService), YourLanguageServiceName, 0, RequestStockColors = true)]
```

#### <a name="to-migrate-a-visual-studio-2008-language-service-to-a-later-version"></a>Visual Studio 2008 言語サービスを新しいバージョンに移行するには

1. 新しいバージョンの Visual Studio と Visual Studio SDK をインストールします。 SDK のインストール方法の詳細については、「[Visual Studio SDK のインストール](../../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

2. RegExLangServ.csproj ファイルを (Visual Studio に読み込まずに) 編集します。

     Microsoft.VsSDK.targets ファイルを参照する `Import` ノードで、値を次のテキストに置き換えます。

    ```
    $(MSBuildExtensionsPath)\Microsoft\VisualStudio\v14.0\VSSDK\Microsoft.VsSDK.targets
    ```

3. ファイルを保存してから閉じます。

4. RegExLangServ.sln ソリューションを開きます。

5. **[一方向のアップグレード]** ウィンドウが表示されます。 **[OK]** をクリックします。

6. プロジェクトのプロパティを更新します。 **ソリューション エクスプローラー** でプロジェクト ノードを選択し、右クリックして **[プロパティ]** を選択して、 **[プロジェクトのプロパティ]** ウィンドウを開きます。

    - **[アプリケーション]** タブの **[ターゲット フレームワーク]** を **[4.6.1]** に変更します。

    - **[デバッグ]** タブの **[外部プログラムを起動する]** ボックスに「 **\<Visual Studio installation path>\Common7\IDE\devenv.exe.** 」と入力します。

         **[コマンドライン引数]** ボックスに「/**rootsuffix Exp**」と入力します。

7. 次の参照を追加します。

    - Microsoft.VisualStudio.Shell.9.0.dll への参照を削除してから、Microsoft.VisualStudio.Shell.14.0.dll と Microsoft.VisualStudio.Shell.Immutable.11.0.dll への参照を追加します。

    - Microsoft.VisualStudio.Package.LanguageService.9.0.dll への参照を削除してから、Microsoft.VisualStudio.Package.LanguageService.14.0.dll への参照を追加します。

    - Microsoft.VisualStudio.Shell.Interop.10.0.dll への参照を追加します。

8. VsPkg.cs ファイルを開き、`DefaultRegistryRoot` 属性の値を次のように変更します。

    ```
    "Software\\Microsoft\\VisualStudio\\14.0Exp"
    ```

9. 元のサンプルにはその言語サービスが登録されていないため、VsPkg.cs に次の属性を追加する必要があります。

    ```
    [ProvideLanguageService(typeof(RegularExpressionLanguageService), "RegularExpressionLanguage", 0, RequestStockColors=true)]
    ```

10. source.extension.vsixmanifest ファイルを追加する必要があります。

    - このファイルを既存の拡張機能からプロジェクト ディレクトリにコピーします (このファイルを取得する方法の 1 つは、VSIX プロジェクトを作成することです ( **[ファイル]** の **[新規]** をクリックしてから、 **[プロジェクト]** をクリックします。 Visual Basic または C# で、 **[拡張機能]** をクリックし、 **[VSIX プロジェクト]** を選択します)。

    - ファイルをプロジェクトに追加します。

    - ファイルの **[プロパティ]** で、 **[ビルド アクション]** を **[なし]** に設定します。

    - **VSIX マニフェスト エディター** でファイルを開きます。

    - 次のフィールドを変更します。

    - **ID**: RegExLangServ

    - **製品名**: RegExLangServ

    - **説明**: 正規表現言語サービス。

    - **[資産]** の **[新規]** をクリックし、 **[種類]** を **[Microsoft.VisualStudio.VsPackage]** に選択し、 **[ソース]** を **[現在のソリューション内のプロジェクト]** に設定し、 **[プロジェクト]** を **[RegExLangServ]** に設定します。

    - ファイルを保存して閉じます。

11. ソリューションをビルドします。 ビルドされたファイルは、 **%USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0Exp\Extensions\MSIT\ RegExLangServ\\** に展開されます。

12. デバッグを開始します。 Visual Studio の 2 つ目のインスタンスが開かれます。

## <a name="see-also"></a>こちらもご覧ください
- [従来の言語サービスの機能拡張](../../extensibility/internals/legacy-language-service-extensibility.md)
