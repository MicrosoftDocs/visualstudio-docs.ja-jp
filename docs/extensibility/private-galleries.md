---
title: プライベート ギャラリー | Microsoft Docs
description: Visual Studio SDK で開発したコントロール、テンプレート、ツールをプライベート ギャラリーに投稿し、共有する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX galleries, private
- private galleries, VSIX
ms.assetid: b6b3dee7-91c5-4556-9f69-0d56b675e83b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c64c5880fcdb1d6a1fb3d6fc7c71f55abf7cbbc1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069037"
---
# <a name="private-galleries"></a>プライベート ギャラリー
開発したコントロール、テンプレート、ツールは、次のように、組織のイントラネット上の *プライベート ギャラリー* に投稿し、共有することができます。

- イントラネット上の適切に構成された中央の場所 (リポジトリ) への Atom (RSS) フィードを作成します。 詳細については、「[方法: プライベート ギャラリーの Atom フィードの作成](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)」を参照してください。

- プライベート ギャラリーについて記述した *.pkgdef* ファイルを配布します。 この構成は、プライベート ギャラリーを同時に多数のコンピューターに接続したい管理者にお勧めです。

## <a name="add-a-private-gallery-to-extensions-and-updates-in-visual-studio"></a>Visual Studio の拡張機能と更新プログラムにプライベート ギャラリーを追加する
 プライベート ギャラリーを使用できるようになったら、Visual Studio で **[拡張機能と更新プログラム]** に追加することができます。

 ![拡張機能マネージャーの追加ダイアログ](../extensibility/media/em_adddialog.png "EM_AddDialog")

### <a name="to-add-a-private-gallery-to-extensions-and-updates"></a>[拡張機能と更新プログラム] にプライベート ギャラリーを追加するには

1. メニュー バーで、 **[ツール]**  >  **[オプション]** の順に選択します。

2. **[環境]** ノードで、 **[拡張機能と更新プログラム]** を選択します。

3. **[追加]** ボタンを選びます。

4. **[名前]** フィールドに、プライベート ギャラリーの名前を入力します (例: `My Gallery`)。

5. **[URL]** フィールドに、プライベート ギャラリーをホストしている Atom フィードまたは SharePoint サイトの URL を入力します。

    1. ホストが、プライベート ギャラリーに接続する Atom フィードである場合、URL は `http://www.mywebsite/mygallery/atom.xml` のようになります。  この URL からは、ファイルまたはネットワーク パスを参照できます。

    2. ホストが SharePoint サイトである場合、URL は `http://mysharepoint/sites/mygallery/forms/AllItems.aspx` のようになります。

### <a name="manage-private-galleries"></a>プライベート ギャラリーを管理する
 管理者は、プライベート ギャラリーを複数のコンピューターで同時に使用できるようにするには、各コンピューター上のシステム レジストリを変更します。 これを実現するには、新しいレジストリ キーとその値を記述した *.pkgdef* ファイルを作成します。  このファイルの形式は次のとおりです。

```
[$RootKey$\ExtensionManager\Repositories\{UniqueGUID}]
@={URI}  (REG_SZ)
Disabled=0 | 1 (DWORD)
Priority=0 (highest priority) ... MaxInt (lowest priority) (DWORD) (uint)
Protocol=Atom|Sharepoint (REG_SZ)
DisplayName={DisplayName} (REG_SZ)
DisplayNameResourceID={ID} (REG_SZ)
DisplayNamePackageGuid={GUID} (REG_SZ)

```

 詳細については、「[方法: レジストリ設定を使用してプライベート ギャラリーを管理する](../extensibility/how-to-manage-a-private-gallery-by-using-registry-settings.md)」を参照してください。

## <a name="install-extensions-from-a-private-gallery"></a>プライベート ギャラリーから拡張機能をインストールする
 **[拡張機能と更新プログラム]** のプライベート ギャラリーから Visual Studio 拡張機能を検索してインストールすることができます。 次の手順では、`My Gallery` という名前のプライベート ギャラリーを使用します。

 ![プライベート ギャラリーをインストールする拡張機能マネージャー](../extensibility/media/em_.png "EM_")

### <a name="to-search-for-and-install-extensions-from-a-private-gallery"></a>プライベート ギャラリーから拡張機能を検索してインストールするには

1. メニュー バーで、 **[ツール]**  >  **[拡張機能と更新プログラム]** を選択します。

2. 左側のペインで **[Online Extensions]\(オンラインの拡張機能\)** を選択し、 **[マイ ギャラリー]** を選択します。

3. 右側のペインで拡張機能を選択し、 **[ダウンロード]** ボタンを選択します。

## <a name="update-extensions-from-a-private-gallery"></a>プライベート ギャラリーから拡張機能を更新する
 Visual Studio 拡張機能の新しいバージョンがプライベート ギャラリーに投稿されると、インストールした拡張機能を更新できます。 次の手順では、`My Repository` という名前のプライベート ギャラリーを使用します。

 ![拡張機能マネージャーのプライベート ギャラリーの更新](../extensibility/media/em_update.png "EM_Update")

### <a name="to-update-an-installed-extension-from-a-private-gallery"></a>インストールされている拡張機能をプライベート ギャラリーから更新するには

1. メニュー バーで、 **[ツール]**  >  **[拡張機能と更新プログラム]** を選択します。

2. 左側のペインで、 **[更新プログラム]** を選択してから、 **[マイ リポジトリ]** を選択します。

3. 右側のペインで拡張機能を選択し、 **[更新]** ボタンを選択します。

## <a name="see-also"></a>こちらもご覧ください
- [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)
- [Visual Studio 拡張機能を配布する](../extensibility/shipping-visual-studio-extensions.md)
