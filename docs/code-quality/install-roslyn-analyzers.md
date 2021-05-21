---
title: サードパーティ製アナライザーのインストール
ms.date: 08/27/2020
description: サードパーティ製のアナライザーを Visual Studio にインストールする方法について説明します。 .vsix ファイルと NuGet アナライザー パッケージのアナライザーをインストールする方法を示します。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 3d4833ba922ddde1a1770cfd75cf446f210e2c79
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859854"
---
# <a name="install-third-party-analyzers"></a>サードパーティ製アナライザーのインストール

Visual Studio には、.NET Compiler Platform (*Roslyn*) アナライザーのコア セットが含まれています。 これらのアナライザーは常に有効になっています。 NuGet パッケージとして、または *VSIX* ファイルの Visual Studio 拡張機能として、追加のアナライザーをインストールできます。

## <a name="to-install-nuget-analyzer-packages"></a>NuGet アナライザー パッケージをインストールするには

1. www.nuget.org でインストールするアナライザー パッケージを見つけます。

   たとえば、[StyleCop.Analyzers](https://www.nuget.org/packages/stylecop.analyzers/) をインストールすることにより、コード ベースでのスタイルの問題を探すことができます。

2. Visual Studio でパッケージをインストールするには、[パッケージ マネージャー コンソール](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)または[パッケージマネージャー UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console) を使用します。

   > [!NOTE]
   > www.nuget.org の各アナライザー パッケージのページには、**パッケージ マネージャー コンソール** に貼り付けるためのコマンドが表示されています。 簡単にテキストをクリップボードにコピーするためのボタンも用意されています。

   アナライザー アセンブリがインストールされ、**ソリューション エクスプローラー** の **[参照]**  >  **[アナライザー]** の下の表示されます。

## <a name="to-install-vsix-analyzers"></a>VSIX アナライザーをインストールするには

::: moniker range="vs-2017"

1. Visual Studio で、 **[ツール]** > **[拡張機能と更新プログラム]** を選択します。

   **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

   > [!NOTE]
   > または、[Visual Studio Marketplace](https://marketplace.visualstudio.com) で直接アナライザー拡張機能を見つけてダウンロードすることもできます。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio で、 **[拡張機能]** > **[拡張機能の管理]** を選択します。

   **[拡張機能の管理]** ダイアログ ボックスが開きます。

   > [!NOTE]
   > または、[Visual Studio Marketplace](https://marketplace.visualstudio.com) で直接アナライザー拡張機能を見つけてダウンロードすることもできます。

::: moniker-end

2. 左側のペインで **[オンライン]** を展開し、 **[Visual Studio Marketplace]** を選択します。

3. 検索ボックスに、インストールするアナライザー拡張機能の名前を入力します。

4. **[ダウンロード]** を選択します。

   拡張機能がダウンロードされます。

5. **[OK]** を選択してダイアログ ボックスを閉じた後、Visual Studio のすべてのインスタンスを閉じて、**VSIX インストーラー** を起動します。

   **[VSIX インストーラー]** ダイアログ ボックスが開きます。

   ![Microsoft Code Analysis 用の VSIX インストーラー](media/vsix-installer-code-analysis.png)

6. **[変更]** を選択すると、インストールが開始されます。

7. インストールは 1 から 2 分で完了します。 **[閉じる]** を選択します。

8. Visual Studio を再度開きます。

::: moniker range="vs-2017"

拡張機能がインストールされているかどうかを確認する場合は、 **[ツール]**  >  **[拡張機能と更新プログラム]** を選択します。 **[拡張機能と更新プログラム]** ダイアログ ボックスで、左側の **[インストール済み]** カテゴリを選択し、名前で拡張機能を検索します。

::: moniker-end

::: moniker range=">=vs-2019"

拡張機能がインストールされているかどうかを確認する場合は、 **[拡張機能]**  >  **[拡張機能の管理]** を選択します。 **[拡張機能の管理]** ダイアログ ボックスで、左側の **[インストール済み]** カテゴリを選択し、名前で拡張機能を検索します。

::: moniker-end

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Visual Studio でコード アナライザーを使用する](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>関連項目

- [Visual Studio のコード アナライザーの概要](../code-quality/roslyn-analyzers-overview.md)
- [.NET アナライザーのインストール](../code-quality/install-net-analyzers.md)
