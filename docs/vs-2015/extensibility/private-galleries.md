---
title: プライベートギャラリー |マイクロソフトドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSIX galleries, private
- private galleries, VSIX
ms.assetid: b6b3dee7-91c5-4556-9f69-0d56b675e83b
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 895fbef5459de75c7ccdc6a090fc30ec27a030f9
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81444922"
---
# <a name="private-galleries"></a>Private Galleries
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

次のように、イントラネットの*プライベート ギャラリー*にポストすることで、開発したコントロール、テンプレート、およびツールを共有できます。  
  
- イントラネット上の適切に構成された中央の場所 (リポジトリ) に Atom (RSS) フィードを作成します。 詳細については、「[方法 : プライベート ギャラリーの Atom フィードを作成する](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)」を参照してください。  
  
- プライベート ギャラリーを記述する .pkgdef ファイルを配布します。 プライベート ギャラリーを複数のコンピュータに同時に接続する管理者には、この構成をお勧めします。  
  
## <a name="adding-a-private-gallery-to-extensions-and-updates-in-visual-studio"></a>Visual Studio での拡張機能と更新プログラムへのプライベート ギャラリーの追加  
 プライベート ギャラリーが使用可能な場合は、Visual Studio の**拡張機能と更新**プログラムに追加できます。  
  
 ![拡張機能マネージャーの追加ダイアログ](../extensibility/media/em-adddialog.png "EM_AddDialog")  
  
#### <a name="to-add-a-private-gallery-to-extensions-and-updates"></a>拡張機能と更新プログラムにプライベート ギャラリーを追加するには  
  
1. メニュー バーで、[**ツール]、[****オプション**] の順に選択します。  
  
2. [**環境**] ノードで、[**拡張機能と更新]** を選択します。  
  
3. **[追加]** をクリックします。  
  
4. [**名前]** フィールドに、プライベート ギャラリーの名前を`My Gallery`入力します。  
  
5. **[URL]** フィールドに、プライベート ギャラリーをホストしている Atom フィードまたは SharePoint サイトの URL を入力します。  
  
    1. ホストがプライベート ギャラリーに接続する Atom フィードの場合、URL は次のようになります。 `http://www.mywebsite/mygallery/atom.xml`  この URL は、ファイルまたはネットワーク パスを参照できます。  
  
    2. ホストが SharePoint サイトの場合、URL は次のようになります。 `http://mysharepoint/sites/mygallery/forms/AllItems.aspx`  
  
### <a name="managing-private-galleries"></a>プライベート ギャラリーの管理  
 管理者は、各コンピュータのシステム レジストリを変更することで、複数のコンピュータでプライベート ギャラリーを同時に利用できるようにすることができます。 これを実現するには、新しいレジストリ キーとその値を記述する .pkgdef ファイルを作成します。  このファイルの形式は以下の通りです。  
  
```  
[$RootPath$\ExtensionManager\Repositories\{UniqueGUID}]  
@={URI}  (REG_SZ)  
Disabled=0 | 1 (DWORD)  
Priority=0 (highest priority) … MaxInt (lowest priority) (DWORD) (uint)  
Protocol=VSGallery|Atom|Sharepoint (REG_SZ)  
DisplayName={DisplayName} (REG_SZ)  
DisplayNameResourceID={ID} (REG_SZ)  
DisplayNamePackageGuid={GUID} (REG_SZ)  
  
```  
  
 詳細については、「 [[方法] レジストリ設定を使用してプライベート ギャラリーを管理する](../extensibility/how-to-manage-a-private-gallery-by-using-registry-settings.md)」を参照してください。  
  
## <a name="installing-extensions-from-a-private-gallery"></a>プライベート ギャラリーからの拡張機能のインストール  
 Visual Studio 拡張機能は、プライベート ギャラリーの**拡張機能と更新プログラム**で検索およびインストールできます。 次の手順では、 という名前`My Gallery`のプライベート ギャラリーを使用します。  
  
 ![プライベート ギャラリーをインストールする拡張機能マネージャー](../extensibility/media/em.png "EM_")  
  
#### <a name="to-search-for-and-install-extensions-from-a-private-gallery"></a>プライベート ギャラリーから拡張機能を検索してインストールするには  
  
1. メニュー バーで、**[ツール]**、**[拡張機能と更新プログラム]** の順にクリックします。  
  
2. 左側のウィンドウで 、[**オンライン拡張機能**] を選択し、[**マイ ギャラリー**] を選択します。  
  
3. 右側のウィンドウで、拡張機能を選択し、[**ダウンロード**] ボタンを選択します。  
  
## <a name="updating-extensions-from-a-private-gallery"></a>プライベート ギャラリーからの拡張機能の更新  
 Visual Studio 拡張機能の新しいバージョンがプライベート ギャラリーにポストされると、インストールされている拡張機能を更新できます。 次の手順では、 という名前`My Repository`のプライベート ギャラリーを使用します。  
  
 ![拡張機能マネージャーのプライベート ギャラリーの更新](../extensibility/media/em-update.png "EM_Update")  
  
#### <a name="to-update-an-installed-extension-from-a-private-gallery"></a>プライベート ギャラリーからインストール済みの拡張機能を更新するには  
  
1. メニュー バーで、**[ツール]**、**[拡張機能と更新プログラム]** の順にクリックします。  
  
2. 左側のウィンドウで [**更新]** を選択し、[**マイ リポジトリ**] を選択します。  
  
3. 右側のウィンドウで、拡張機能を選択し、[**更新**] ボタンを選択します。  
  
## <a name="see-also"></a>参照  
 [ビジュアル スタジオ拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)   
 [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)
