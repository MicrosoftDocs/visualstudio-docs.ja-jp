---
title: '方法: IIS のプロパティ設定を確認します |。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- IIS, property settings
- debugging Web applications, troubleshooting
- IIS administration tool
- Web applications, setting properties
- properties [debugger], setting with IIS administration tool
ms.assetid: 9efc50bf-02fb-4750-9b3e-f03c38f10d8b
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 075581332a95f8cae03313adaf5fc2067910b217
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58962610"
---
# <a name="how-to-verify-iis-property-settings"></a>方法: IIS のプロパティ設定を確認する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

IIS 管理ツールで、Web アプリケーションのプロパティを設定できます。 これらのプロパティは、実行するアプリケーションに合わせて正しく設定する必要があります。そのため、トラブルシューティングのときに、多くの場合、設定を確認することが必要になります。  
  
> [!NOTE]
>  実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](http://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
### <a name="to-check-iis-settings-for-the-web-application"></a>Web アプリケーションの IIS 設定をチェックするには  
  
1.  開く、**管理ツール**ウィンドウ。**開始**メニューで、**プログラム**、 をクリックし、**管理ツール**。 場合**管理ツール**に表示されない、**プログラム**メニューから、[検索対象] で、**コントロール パネルの**です。  
  
    -   Windows 2000 では、**[インターネット サービス マネージャー]** を選択します。  
  
    -   Windows XP では、**[インターネット インフォメーション サービス]** を選択します。  
  
    -   Windows Server 2003 では、**[サーバーの管理]** をダブルクリックします。  
  
         **[サーバーの管理]** ウィンドウが開きます。 **[アプリケーション サーバー]** の下にある **[このアプリケーション サーバーを管理する]** をクリックします。  
  
         **[アプリケーション サーバー]** ウィンドウが開きます。 左側のペインで、**[インターネット インフォメーション サービス (IIS) マネージャー]** ノードを開きます。  
  
2.  ダイアログ ボックスで、使用しているコンピューターのツリー コントロール ノードをクリックします。 **[Web サイト]** ノードをクリックし、Web アプリケーションのノードを選択します。 このノードは、[Web サイト] ノード (**[既定の Web サイト]** ノードの兄弟ノード)、または既存の Web サイト ノード下にある仮想ディレクトリ ノードのいずれかになります。  
  
3.  Web アプリケーションを右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。  
  
4.  Web アプリケーションのセキュリティ設定を確認します。  
  
    1.  Web アプリケーションの **[プロパティ]** ウィンドウで、**[ディレクトリ セキュリティ]** タブをクリックし、**[編集]** をクリックします。  
  
    2.  **[認証方法]** ダイアログ ボックスで、**[匿名アクセスを有効にする]** および **[統合 Windows 認証]** を選択します (選択されていない場合)。  
  
    3.  **[OK]** をクリックして **[認証方法]** ダイアログ ボックスを閉じます。  
  
5.  ATL Server アプリケーションの場合は、DEBUG の動詞が ISAPI 拡張機能に関連付けられていることを確認してください。 詳細については、「[方法 :拡張機能と DEBUG 動詞を関連付ける](http://msdn.microsoft.com/50d261d3-4bd4-41c0-b44e-3591086f121e)します。  
  
6.  [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] アプリケーションの場合、アプリケーションの仮想フォルダーに、**インターネット インフォメーション サービス (IIS) マネージャー**、**インターネット サービス マネージャー**、または**インターネット インフォメーション サービス**で設定されたアプリケーション名があることを確認します。  
  
    1.  Web アプリケーションの **[プロパティ]** ウィンドウで、**[ディレクトリ]** タブ (アプリケーションが仮想ディレクトリにある場合) または **[ホーム ディレクトリ]** タブ (アプリケーションが Web サイトにある場合) を選択します。  
  
    2.  **[ローカル パス]** の名前が、アプリケーションを実際に配置したディレクトリ名と一致することを確認します。  
  
    3.  **[アプリケーションの設定]** の下に、アプリケーションが格納されている root ディレクトリの名前を入力します。  
  
    4.  **[OK]** をクリックして、**[プロパティ]** ダイアログ ボックスを閉じます。  
  
7.  [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]アプリケーションでは、をクリックして、 **ASP.NET** タブであることを確認し、正しいバージョンの[!INCLUDE[vstecasp](../includes/vstecasp-md.md)]が指定されています。  
  
8.  **[OK]** をクリックして、**[プロパティ]** ダイアログ ボックスを閉じます。  
  
9. **[OK]** をクリックして、**[インターネット インフォメーション サービス (IIS) マネージャー]**、**[インターネット サービス マネージャー]**、または **[インターネット インフォメーション サービス]** の各ダイアログ ボックスを閉じます。  
  
## <a name="see-also"></a>関連項目  
 [トラブルシューティング](../debugger/debugging-web-applications-troubleshooting.md)
