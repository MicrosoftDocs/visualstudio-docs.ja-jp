---
title: Visual Basic 開発者設定を使用してビルド構成を管理する
ms.date: 11/21/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-compile
ms.topic: conceptual
helpviewer_keywords:
- advanced build configurations
- building with Visual Basic developer settings (Visual Studio)
- debug builds
- release builds
ms.assetid: eaea6e0b-6c61-4869-8d63-d372c745a23c
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 92ff0f0d79657855667c260754bbc4a9857fec83
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54985852"
---
# <a name="how-to-manage-build-configurations-with-visual-basic-developer-settings-applied"></a>方法: Visual Basic 開発者設定が適用されたビルド構成を管理する

既定では、Visual Studio 開発者設定が適用されると、すべてのビルド構成の詳細オプションが非表示になります。 この記事では、これらのビルド設定を手動で有効にする方法について説明します。

## <a name="enable-advanced-build-configurations"></a>ビルド構成の詳細を有効にする

既定では、**[構成マネージャー]** ダイアログ ボックスおよび[プロジェクト デザイナー](../ide/reference/application-page-project-designer-visual-basic.md)の **[構成]** 一覧と **[プラットフォーム]** 一覧を開くためのオプションは、Visual Basic 開発者設定によって非表示になっています。

1.  **[ツール]** メニューの **[オプション]** をクリックします。

2.  **[プロジェクトおよびソリューション]** を展開し、**[全般]** をクリックします。

    > [!NOTE]
    > **[全般]** ノードは、**[すべての設定を表示]** オプションがオフになっている場合でも表示されます。 使用可能なすべてのオプションを表示する場合は、**[すべての設定を表示]** をクリックします。

3.  **[ビルド構成の詳細を表示]** をクリックします。

4.  **[OK]** をクリックします。

     **[ビルド]** メニューで **[構成マネージャー]** を使用できるようになり、**[構成]** 一覧と **[プラットフォーム]** 一覧が**プロジェクト デザイナー**に表示されるようになります。

## <a name="see-also"></a>関連項目

- [ビルド構成について](../ide/understanding-build-configurations.md)
- [コンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
- [環境設定](../ide/environment-settings.md)