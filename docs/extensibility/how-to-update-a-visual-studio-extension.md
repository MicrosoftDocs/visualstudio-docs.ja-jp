---
title: '方法: Visual Studio 拡張機能を更新する | Microsoft Docs'
description: 拡張機能と更新プログラムを使用して、更新されたバージョンをインストールすることにより、システムの Visual Studio 拡張機能を更新する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- update package
- update extension
- new package version
ms.assetid: 93f79774-7b79-4dd6-94ad-13698f72c257
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e2af6217ac2f056461c6d833de5d804ebdab17b6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074861"
---
# <a name="how-to-update-a-visual-studio-extension"></a>方法: Visual Studio 拡張機能を更新する
**拡張機能と更新プログラム** を使用して、更新されたバージョンをインストールすることにより、システムの Visual Studio 拡張機能を更新できます。 拡張機能の更新されたバージョンを作成した場合、VSIX マニフェストのバージョン番号をインクリメントして、更新済みとしてそれを表すことができます。

 受信した拡張機能の VSIX マニフェストが、インストールされているものと同じ `ID` で、`Version` 番号が大きい場合に、更新プログラムがインストールされます。 `Version` 番号が同じか小さい場合は、パッケージをインストールできません。 `ID` 値が一致しない場合、まだインストールされていないパッケージは個別の拡張機能として認識されます。

 開発中の競合を防ぐために、処理中の拡張機能の以前のバージョンをアンインストールし、さらに競合する可能性のある拡張機能もアンインストールするか無効にすることが推奨されます。

## <a name="to-update-an-extension-on-your-system"></a>システム上の拡張機能を更新するには

1. **[ツール]** メニューの **[拡張機能と更新プログラム]** をクリックします。

2. 左側のウィンドウで、 **[更新]** をクリックします。

3. 中央のウィンドウで、インストールする更新プログラムをクリックします。

     更新された拡張機能のバージョン番号が、その他の情報と共に右側のウィンドウに表示されます。

4. 右側のウィンドウの下部で **[更新]** をクリックします。

## <a name="to-publish-an-update-of-an-extension"></a>拡張機能の更新プログラムを公開するには

1. Visual Studio で、更新する拡張機能のソリューションを開きます。 変更を行います。

    > [!IMPORTANT]
    > 未署名のすべてのユーザー拡張機能は自動的に更新されません。 常に拡張機能に署名する必要があります。

2. **ソリューション エクスプローラー** で、 *[source.extension.manifest]* を開きます。

3. マニフェスト デザイナーで、 **[バージョン]** フィールドの値を増やします。

4. ソリューションを保存してビルドします。

5. 新しい *.vsix* ファイル (プロジェクトの *\bin\Debug\* フォルダー内) を [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) Web サイトにアップロードします。

     以前のバージョンの拡張機能を使用しているユーザーが、 **[拡張機能と更新プログラム]** を開くと、ツールが自動的に更新プログラムを検索するように設定されていれば、新しいバージョンが **[更新プログラム]** リストに表示されます。

     **[更新プログラム]** ウィンドウの下部で、更新プログラムの自動確認を有効または無効にできます ( **[使用可能な更新プログラムの自動検出の有効化] または [利用可能な更新プログラムの自動検出を無効にする]** )。これにより、 **[ツール]**  >  **[オプション]**  >  **[環境]**  >  **[拡張機能と更新プログラム]** の **[更新プログラムの確認]** 設定が変更されます。

    > [!NOTE]
    > Visual Studio 2015 更新プログラム 2 より、ユーザー単位の拡張機能を自動更新するか、すべてのユーザー拡張機能を更新するか、両方を行うか (既定の設定) 指定できます ( **[ツール]**  >  **[オプション]**  >  **[環境]**  >  **[拡張機能と更新プログラム]** )。

## <a name="see-also"></a>関連項目
- [VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)
- [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)
