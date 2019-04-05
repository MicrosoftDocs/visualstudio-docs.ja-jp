---
title: 'チュートリアル: カスタム エディターの作成 |Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], custom - create
ms.assetid: d090abb6-d99f-4083-a3db-cd16bf81ce7d
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0b7c8bd8643b6c670e614f4745650f42ccca35f5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51809741"
---
# <a name="walkthrough-creating-a-custom-editor"></a>チュートリアル: カスタム エディターを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage プロジェクト テンプレートは、C++ では、単純なカスタム エディターを作成できます。  VSPackage プロジェクト テンプレートは、c# または Visual Basic のプロジェクトをサポートしていません。 詳細については、[Visual Studio SDK](../extensibility/visual-studio-sdk.md)を参照してください。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルに従うには、Visual Studio SDK をインストールする必要があります。 より詳細な情報については 、[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md) に関する記事を参照してください。  
  
## <a name="the-visual-studio-package-project-template"></a>Visual Studio パッケージ プロジェクト テンプレート  
 Visual Studio パッケージ プロジェクト テンプレートが記載されて、**新しいプロジェクト**C++ 拡張機能フォルダーのダイアログ  
  
### <a name="to-create-a-vspackage-using-the-visual-studio-package-template"></a>Visual Studio パッケージ テンプレートを使用して VSPackage を作成するには  
  
1.  Visual Studio パッケージ テンプレートを使用してプロジェクトを作成します。  
  
2.  選択、**カスタム エディター**オプションを選択し、をクリックして**次**します。 **エディター オプション**ページが表示されます。  
  
3.  エディターの名前を入力、**エディター名**ボックス。 エディターに関連付けるファイル拡張子を入力、**ファイル拡張子**ボックス。 エディターでは、この拡張機能を持つファイル使用できます。 ファイル拡張機能は Windows ではなくのみ、Visual Studio の登録します。 エディターで作成された新しいドキュメントの既定のファイル名を入力、**既定のファイル名**ボックス。  
  
4.  **[完了]** をクリックして、指定したフォルダーに VSPackage を作成します。  
  
### <a name="to-test-your-custom-editor"></a>カスタム エディターをテストするには  
  
1.  **ファイル**メニューで、**新規** をクリックし、**ファイル**します。  
  
2.  **インストールされたテンプレート**のウィンドウ、**新しいファイル**ダイアログ ボックスを選択し、ファイル テンプレート、ファイルの種類を登録します。  
  
3.  クリックして**オープン**ドキュメントを表示および編集します。  
  
     エディターには、切り取りと貼り付け、検索と置換、およびオープン アンド ロード操作がサポートしています。  
  
## <a name="see-also"></a>関連項目  
 [VSPackage](../extensibility/internals/vspackages.md)

