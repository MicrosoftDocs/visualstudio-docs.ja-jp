---
title: '方法: VSIX パッケージへの依存関係の追加 | Microsoft Docs'
description: ターゲット コンピューターにまだ存在しない依存関係をインストールする VSIX パッケージの配置を設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- package reference
- package assembly
- package dll
- vsix reference
ms.assetid: 8f20177b-dab9-43a3-b959-81a591b451d6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 48c6ac0abd5ffb6c36dc894829e29c9304563a5e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057404"
---
# <a name="how-to-add-a-dependency-to-a-vsix-package"></a>方法: VSIX パッケージへの依存関係の追加

ターゲット コンピューターにまだ存在しない依存関係をインストールする VSIX パッケージの配置を設定することができます。 これを実現するには、VSIX の依存関係を *source.extension.vsixmanifest* ファイルに追加します。

## <a name="to-add-a-dependency"></a>依存関係を追加する方法

1. **[デザイン]** ビューで *source.extension.vsixmanifest* ファイルを開きます。 **[依存関係]** タブにアクセスし、 **[新規]** をクリックします。

2. インストールされている拡張機能を追加するには、 **[新しい依存関係の追加]** ダイアログ ボックスで **[インストールされている拡張機能]** を選択し、 **[名前]** に一覧にある拡張子を選択します。

3. インストールされていない別の VSIX を追加するには、 **[新しい依存関係の追加]** ダイアログ ボックスで、 **[ファイル システム上のファイル]** を選択し、 **[参照]** ボタンを使用して VSIX を選択します。

## <a name="require-a-specific-visual-studio-release"></a>特定の Visual Studio リリースを要求する

拡張機能に特定のバージョンの Visual Studio 2017 が必要な場合、たとえば、15.3 でリリースされた機能に依存している場合は、VSIX **インストール ターゲット** でビルド番号を指定できます。 たとえば、リリース 15.3 のビルド番号は '15.0.26730.3' です。 [ここで](../install/visual-studio-build-numbers-and-release-dates.md)、リリースからビルド番号へのマッピングを確認できます。 リリース番号 '15.3' を使用しても適切に機能しないことに注意してください。

拡張機能に 15.3 以上が必要な場合は、**InstallationTarget Version** を次のように [15.0.26730.3, 16.0) として宣言します。

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```

VSIXInstaller は、以前のバージョンの Visual Studio を検出し、後で更新する必要があることをユーザーに通知します。

## <a name="see-also"></a>関連項目

- [VSIX 拡張機能スキーマ 1.0 リファレンス](/previous-versions/dd393700(v=vs.110))
- [VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)
- [Windows インストーラーの配置に関する拡張機能を準備する](../extensibility/preparing-extensions-for-windows-installer-deployment.md)