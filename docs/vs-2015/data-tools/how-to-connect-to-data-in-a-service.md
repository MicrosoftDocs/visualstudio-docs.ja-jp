---
title: '方法: データ サービスに接続する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], connecting to Web services
- data sources, creating from Web services
- data [Visual Studio], reading from Web services
- reading data, from Web services
- Web services, reading data
- Web services, as data sources
- Web services, connecting
ms.assetid: a6b54353-05fe-4e5c-8631-90231fc95504
caps.latest.revision: 35
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e3361ba51607924ee0bd0701f6f2dddf12334f93
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60090382"
---
# <a name="how-to-connect-to-data-in-a-service"></a>方法: サービスのデータに接続する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーションを実行して、サービスから返されたデータを接続する、[データ ソース構成ウィザード](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f)選択**サービス**上、 **のデータソースの種類を選択**ページ。  
  
 ウィザードの完了したら、サービス参照をプロジェクトに追加されですぐに使用できるは、[データ ソース ウィンドウ](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)します。  
  
> [!NOTE]
>  **[データ ソース]** ウィンドウに表示される項目は、サービスから返される情報に応じて異なります。 サービスによっては、**データ ソース構成ウィザード**でバインドできるオブジェクトを作成するための十分な情報を提供しないものもあります。 たとえば、サービスには、データセットが返された場合その項目に表示できません、**データ ソース ウィンドウ**ウィザードを完了するとします。 これは、ウィザードには、データ ソースを作成するのに十分な情報がないため、型指定されていないデータセットがスキーマで提供されないためにです。  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
### <a name="to-connect-your-application-to-a-service"></a>アプリケーション サービスに接続するには  
  
1. **[データ]** メニューの **[新しいデータ ソースの追加]** をクリックします。  
  
2. 選択**サービス**上、**データ ソースの種類を選択**] ページの [クリックして **[次へ]**。  
  
3. 使用して、またはをクリックする、サービスのアドレスを入力**Discover**をクリックして、現在のソリューションでのサービスを探します**移動**します。  
  
4. 必要に応じて、新しい**Namespace**既定値の代わりに型指定することができます。  
  
    > [!NOTE]
    >  をクリックして**詳細**を開く、[サービス参照の構成 ダイアログ ボックス](../data-tools/configure-service-reference-dialog-box.md)します。  
  
5. をクリックして**OK**をプロジェクトにサービス参照を追加します。  
  
6. **[完了]** をクリックします。  
  
     **[データ ソース]** ウィンドウに、データ ソースが追加されます。  
  
## <a name="next-steps"></a>次の手順  
  
#### <a name="to-add-functionality-to-your-application"></a>アプリケーションに機能を追加するには  
  
- 項目を選択、**データソース**ウィンドウ バインドされたコントロールを作成するためのフォームにドラッグします。 詳細については、次を参照してください。 [Visual Studio でのデータ コントロールをバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)します。  
  
## <a name="see-also"></a>関連項目  
 [WCF データ サービスへの WPF コントロールをバインドします。](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)   
 [Visual Studio での Windows Communication Foundation サービスと WCF データ サービス](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
