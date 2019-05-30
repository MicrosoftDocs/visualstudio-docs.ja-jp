---
title: '方法: Visual Studio 拡張機能の更新 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- update package
- update extension
- new package version
ms.assetid: 93f79774-7b79-4dd6-94ad-13698f72c257
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 237a1139a7a314cf99b5edbd8993abefe04592c8
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66324871"
---
# <a name="how-to-update-a-visual-studio-extension"></a>方法: Visual Studio 拡張機能を更新します。
使用して、システムに Visual Studio 拡張機能を更新する**拡張機能と更新**更新されたバージョンをインストールします。 VSIX マニフェストのバージョン番号をインクリメントして更新されるとは、拡張機能の更新バージョンを作成する場合を示すことができます。

 同じ入力方向の拡張機能の VSIX マニフェストであるときに更新プログラムがインストールされている`ID`として 1 つずつインストールしより高度な`Version`数。 場合、`Version`番号は、同じまたは低い、パッケージをインストールすることはできません。 場合、`ID`値が一致しない場合、まだインストールされていないパッケージは、別個の拡張機能として認識します。

 開発中に競合を防ぐため、進行中で拡張機能の以前のバージョンをアンインストールしてもアンインストールまたは競合する可能性があるその他のすべての拡張機能を無効にお勧めします。

## <a name="to-update-an-extension-on-your-system"></a>システムに拡張機能を更新するには

1. **[ツール]** メニューの **[拡張機能と更新プログラム]** をクリックします。

2. 左側のウィンドウで次のようにクリックします。**更新**します。

3. 中央のペインで、インストールする更新プログラムをクリックします。

     更新された拡張機能のバージョン番号は、その他の情報と共に、右側のウィンドウに表示されます。

4. 右側のウィンドウの下部には、次のようにクリックします。 **Update**します。

## <a name="to-publish-an-update-of-an-extension"></a>拡張機能の更新を発行するには

1. Visual Studio で、拡張機能を更新するためのソリューションを開きます。 変更を行います。

    > [!IMPORTANT]
    > 未署名のすべてのユーザー拡張機能は自動的に更新されません。 常に、拡張機能に署名する必要があります。

2. **ソリューション エクスプ ローラー**オープン*source.extension.manifest*します。

3. マニフェスト デザイナーでの番号の値を増やす、**バージョン**フィールド。

4. ソリューションを保存してビルドします。

5. 新しいアップロード *.vsix*ファイル (で、* \bin\Debug\*プロジェクトのフォルダー) に、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) Web サイト。

     拡張機能の以前のバージョンを持つユーザーが開いたとき**拡張機能と更新プログラム**、新しいバージョンが表示されます、**更新**ツールが自動的に更新プログラムを探すように設定されている、一覧表示します。

     有効にまたはの下部にある更新プログラムの自動チェックを無効にすることができます、**更新**ウィンドウ (**使用可能な更新プログラムの自動検出を有効または無効に**)、変更、**の確認更新プログラム**設定**ツール** > **オプション** > **環境** >  **拡張機能と更新**します。

    > [!NOTE]
    > Visual Studio 2015 Update 2 以降を指定できます (で**ツール** > **オプション** > **環境** >  **拡張機能と更新**) ユーザー単位の拡張、すべてのユーザー拡張機能、または両方 (既定の設定) の自動更新をするかどうか。

## <a name="see-also"></a>関連項目
- [VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)
- [検索と Visual Studio 拡張機能を使用します。](../ide/finding-and-using-visual-studio-extensions.md)