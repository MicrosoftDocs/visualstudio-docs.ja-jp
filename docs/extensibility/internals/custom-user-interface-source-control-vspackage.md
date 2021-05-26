---
title: カスタム ユーザー インターフェイス (ソース管理 VSPackage) | Microsoft Docs
description: ソース管理 VSPackage を使用して UI 要素を指定して、Visual Studio でカスタム ユーザー インターフェイス (UI) を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interface, source control packages
- source control packages, user interface
ms.assetid: f35ddb24-53bf-461e-b34f-7414f657c082
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1239b11e814ba08e4e481358f5e7fdd0e5dc666b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091033"
---
# <a name="custom-user-interface-source-control-vspackage"></a>カスタム ユーザー インターフェイス (ソース管理 VSPackage)
VSPackage では、Visual Studio のコマンド テーブル ( *.vsct*) ファイルを使用して、そのメニュー項目と既定の状態を宣言します。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) には、VSPackage が読み込まれるまで、既定の状態でメニュー項目が表示されます。 その後、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドを呼び出して、メニュー項目を有効または無効にします。

 VSPackage では、コマンドのユーザー インターフェイス (UI) コンテキストに応じて VSPackage を自動的に読み込むことができるようにレジストリ キーを設定できます。ただし、ソース管理 VSPackage では通常、特定の UI コンテキストに切り替えるだけではなく、必要に応じて読み込みを行う必要があります。 **AutoLoadPackages** レジストリ キーの詳細については、「[VSPackage を管理する](../../extensibility/managing-vspackages.md)」を参照してください。

## <a name="vspackage-ui"></a>VSPackage UI
 ソース管理パッケージは VSPackage として実装され、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の UI は使用されません。 各ソース管理 VSPackage では、メニュー項目、メニュー グループ、ツール ウィンドウ、ツールバー、ソース管理 VSPackage に固有のオプションを設定するために必要な UI など、独自の UI 要素を指定する必要があります。 これらの UI 要素は、静的または動的に有効にすることができます。 静的 UI 要素は *.vsct* ファイルで定義され、VSPackage が読み込まれているかどうかにかかわらず表示されます。 動的 UI 要素は、<xref:EnvDTE.Constants.vsContextNoSolution> などの特定のコマンド UI コンテキストに応じて、または <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドの呼び出しの結果として表示される場合があります。 動的 UI 要素の可視性は、VSpackage の遅延読み込みの方法に準拠しています。

## <a name="ui-constraints-on-source-control-vspackages"></a>ソース管理 VSpackage の UI 制約
 ソース管理 VSPackage は、読み込まれた後に IDE から削除できないため、VSPackage は非アクティブ状態になることができる必要があります。 アクティブでなくなったという通知を VSPackage で受信すると、VSPackage ではその UI を無効にし、外部の IDE との対話を無視します。 VSPackage による <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドの実装では、VSPackage がアクティブでない場合にコマンドを非表示にする必要があります。

 すべてのソース管理 VSPackage では、`IVsSccProvider` インターフェイスを実装する必要があります。 VSPackage によって、インターフェイスの 2 つのメソッドである <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A> を実装する必要があります。

 ソース管理 VSPackage では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> や <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> などによって実装されるさまざまな IDE イベントをサブスクライブしている場合があります。 また、VSPackage では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> などのレジストリ対応のコールバック インターフェイスを実装している場合もあります。 これらのインターフェイスはすべて、非アクティブなときは無視する必要があります。

 次の一覧は、ソース管理 VSPackage のアクティブ状態の影響を受けるインターフェイスを示しています。

- トラック プロジェクト ドキュメント イベント。

- ソリューション イベント。

- ソリューション永続化インターフェイス。 非アクティブの場合、パッケージでは *.sln* と *.suo* ファイルに書き込むことはできません。

- プロパティ エクステンダー。

  ソース管理 VSPackage が非アクティブになっている場合、必須の <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>、およびソース管理に関連付けられているオプションのインターフェイスは呼び出されません。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE が起動すると、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、コマンド UI コンテキストが現在の既定のソース管理 VSPackage ID の ID に設定されます。 これにより、アクティブなソース管理 VSPackage の静的 UI が、実際には VSPackage を読み込まずに IDE に表示されます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、VSPackage の呼び出しを行う前に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider> を介して VSPackage が [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に登録されるのを一時停止します。

  次の表は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE でさまざまな UI 項目が非表示にされる方法についての詳細を示しています。

| UI 項目 | 説明 |
| - | - |
| メニューとツールバー | ソース管理パッケージでは、最初のメニューとツールバーの表示状態を、 *.vsct* ファイルの [VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) セクションでソース管理パッケージ ID に設定する必要があります。 これにより、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE では、VSPackage を読み込んで <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドの実装を呼び出さなくても、メニュー項目の状態を適切に設定できます。 |
| ツール ウィンドウ | ソース管理 VSPackage では、非アクティブにされたときに所有しているすべてのツール ウィンドウを非表示にします。 |
| ソース管理 VSPackage 固有のオプション ページ | レジストリキー **HKLM\SOFTWARE\Microsoft\VisualStudio\X.Y\ToolsOptionsPages\VisibilityCmdUIContexts** を使用すると、オプション ページを表示する必要があるコンテキストを VSPackage で設定できます。 このキーの下にあるレジストリ エントリを作成するには、ソース管理サービスのサービス ID (SID) を使用して、それに DWORD 値 1 を割り当てる必要があります。 ソース管理 VSPackage が登録されているコンテキストで UI イベントが発生するときは常に、VSPackage がアクティブな場合は呼び出されます。 |

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>
- <xref:EnvDTE.Constants.vsContextNoSolution>
- [VSPackage を管理する](../../extensibility/managing-vspackages.md)
