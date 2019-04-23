---
title: オプション ページの作成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- managed package framework, creating Tools Options pages
- Tools Options pages [Visual Studio SDK], creating using managed package framework
ms.assetid: 1bf11fec-dece-4943-8053-6de1483c43eb
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8c2b993a6c6947adfa3b01f2947b992b23236b8f
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60106125"
---
# <a name="creating-options-pages"></a>オプション ページの作成
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Managed package framework から派生したクラス<xref:Microsoft.VisualStudio.Shell.DialogPage>拡張、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]を追加して IDE**オプション**ページの下で、**ツール**メニュー。  
  
 実装するオブジェクトを指定した**ツール オプション**ページは、特定の Vspackage に関連付け、<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>オブジェクト。  
  
 環境は、特定の実装のオブジェクトをインスタンス化するため**ツール オプション**IDE によって特定のページが表示されるときにページします。  
  
- A**ツール オプション**独自のオブジェクトでは、VSPackage を実装するオブジェクトではなく、ページを実装する必要があります。  
  
- オブジェクトは、複数を実装できません**ツール オプション**ページ。  
  
## <a name="registering-as-a-tools-options-page-provider"></a>ツール オプション ページ プロバイダーとして登録します。  
 VSPackage サポート ユーザー構成を通じて**ツール オプション**ページを提供するオブジェクトを示します**ツール オプション**のインスタンスを適用することでページ<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>に適用される<xref:Microsoft.VisualStudio.Shell.Package>実装します。  
  
 1 つのインスタンスが必要があります<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>のすべて<xref:Microsoft.VisualStudio.Shell.DialogPage>-派生型を実装する、**ツール オプション**ページ。  
  
 各インスタンス<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>を実装する型を使用して、**ツール オプション**ページのカテゴリとサブカテゴリを識別するために使用を含む文字列を**ツール オプション**ページ、およびリソース情報として提供する型を登録する、**ツール オプション**ページ。  
  
## <a name="persisting-tools-options-page-state"></a>ツール オプション ページの状態を保持します。  
 場合、**ツール オプション**オートメーションのサポートが有効なページの実装が登録されて、IDE と他のすべてのページの状態が解決しない**ツール オプション**ページ。  
  
 VSPackage を使用して、独自の永続化を管理できる<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>します。 1 つだけまたは永続化のもう一方のメソッドを使用する必要があります。  
  
## <a name="implementing-dialogpage-class"></a>DialogPage クラスを実装します。  
 VSPackage の実装を提供するオブジェクト、 <xref:Microsoft.VisualStudio.Shell.DialogPage>-派生型は次の継承された機能を利用できます。  
  
- 既定のユーザー インターフェイス ウィンドウです。  
  
- 既定の永続化メカニズムの使用可能な場合<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>、クラスに適用される場合は、<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute.SupportsProfiles%2A>プロパティに設定されて`true`の<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>クラスに適用されています。  
  
- オートメーションをサポートします。  
  
  実装するオブジェクトの最小要件を**ツール オプション**ページを使用して<xref:Microsoft.VisualStudio.Shell.DialogPage>パブリック プロパティを追加します。  
  
  クラスとして正しく登録されている場合、**ツール オプション**プロバイダーは、そのパブリック プロパティが 利用可能なページ、**オプション**のセクション、**ツール**のフォームのメニューで、プロパティ グリッドです。  
  
  これらすべての既定の機能を無効にできます。 たとえばより高度なユーザーを作成するインターフェイス必要がありますのみの既定の実装をオーバーライドする<xref:Microsoft.VisualStudio.Shell.DialogPage.Window%2A>します。  
  
## <a name="example"></a>例  
 オプション ページの単純な"hello world"実装は、次に示します。 Visual Studio パッケージ テンプレートによって作成された既定のプロジェクトに次のコードを追加、**メニュー コマンド**オプションを選択したはオプション ページの機能に適切に紹介します。  
  
### <a name="description"></a>説明  
 次のクラスは、最小限の"hello world"オプション ページを定義します。 ユーザーがパブリックに設定できる開かれると、`HelloWorld`プロパティ グリッドでプロパティ。  
  
### <a name="code"></a>コード  
 [!code-csharp[UI_UserSettings_ToolsOptionPages#11](../../snippets/csharp/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/cs/class1.cs#11)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#11](../../snippets/visualbasic/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/vb/class1.vb#11)]  
  
### <a name="description"></a>説明  
 パッケージ クラスに次の属性を適用するページのオプション使用できるように、パッケージの読み込み時にします。 数値は、カテゴリと、ページの任意のリソース Id と、最後にブール値では、ページがオートメーションをサポートしているかどうかを指定します。  
  
### <a name="code"></a>コード  
 [!code-csharp[UI_UserSettings_ToolsOptionPages#07](../../snippets/csharp/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/cs/uiusersettingstoolsoptionspagespackage.cs#07)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#07](../../snippets/visualbasic/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/vb/uiusersettingstoolsoptionspagespackage.vb#07)]  
  
### <a name="description"></a>説明  
 次のイベント ハンドラーでは、[オプション] ページで設定のプロパティの値に応じて結果が表示されます。 使用して、<xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A>ページによって公開されるプロパティにアクセスするカスタム オプション ページの種類に結果を持つメソッドが明示的にキャストします。  
  
 パッケージ テンプレートによって生成されたプロジェクトの場合からこの関数を呼び出し、`MenuItemCallback`既定コマンドに接続する関数に追加、**ツール**メニュー。  
  
### <a name="code"></a>コード  
 [!code-csharp[UI_UserSettings_ToolsOptionPages#08](../../snippets/csharp/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/cs/uiusersettingstoolsoptionspagespackage.cs#08)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#08](../../snippets/visualbasic/VS_Snippets_VSSDK/ui_usersettings_toolsoptionpages/vb/uiusersettingstoolsoptionspagespackage.vb#08)]  
  
## <a name="see-also"></a>関連項目  
 [拡張ユーザー設定とオプション](../../extensibility/extending-user-settings-and-options.md)   
 [オプション ページのオートメーションのサポート](../../extensibility/internals/automation-support-for-options-pages.md)
