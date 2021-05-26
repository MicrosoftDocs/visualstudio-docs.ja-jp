---
title: 'チェック リスト: 従来の言語サービスの作成 | Microsoft Docs'
description: Visual Studio コア エディターのレガシ言語サービスを作成するために必要な基本手順について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services
- language services, native code
ms.assetid: 8b73b341-a33a-4ab5-9390-178c9e563d2d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 111e72714f4afd56b7b53e9cc48329ba6ce68162
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074796"
---
# <a name="checklist-create-a-legacy-language-service"></a>チェック リスト: 従来の言語サービスの作成
次のチェック リストに、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コア エディターの言語サービスを作成するために必要な基本手順をまとめています。 言語サービスを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に統合するには、デバッグ式エバリュエーターを作成する必要があります。 詳細については、「[Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)」の[CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)に関するページを参照してください。

## <a name="steps-to-create-a-language-service"></a>言語サービスを作成する手順

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> インターフェイスを実装します。

    - VSPackage で、言語サービスを提供する <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> インターフェイスを実装します。

    - <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 実装の統合開発環境 (IDE) で言語サービスを使用できるようにします。

2. メイン言語サービス クラスに <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> インターフェイスを実装します。

     <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> インターフェイスは、コア エディターと言語サービス間の対話の開始点です。

### <a name="optional-features"></a>オプション機能
 次の機能は省略可能であり、任意の順序で実装できます。 これらの機能により、言語サービスの機能性が高まります。

- 構文の色分け表示

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> インターフェイスを実装します。 このインターフェイスの実装では、パーサー情報で適切な色情報を返す必要があります。

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> メソッドは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> インターフェイスを返します。 テキスト バッファーごとに個別のカラーライザー インスタンスが作成されるため、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> インターフェイスを個別に実装する必要があります。 詳細については、[従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)に関するページを参照してください。

- [コード ウィンドウ]

  新しいコード ウィンドウが作成されたときに、言語サービスで通知を受け取ることができるように、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> インターフェイスを実装します。

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> メソッドは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> インターフェイスを返します。 それにより、言語サービスでは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A> でコード ウィンドウに特殊な UI を追加できます。 さらに、言語サービスでは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.OnNewView%2A> でテキスト ビュー フィルターを追加するなど、特別な処理を行うこともでき ます。

- テキスト ビュー フィルター

  言語サービスで IntelliSense ステートメント入力候補を提供するには、それ以外の場合にテキスト ビューで処理されるコマンドの一部をインターセプトする必要があります。 これらのコマンドをインターセプトするには、次の手順を実行します。

  - コマンド チェーンに参加し、エディターのコマンドを処理するために、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> を実装します。

  - <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> メソッドを呼び出し、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 実装を渡します。

  - ビューからデタッチするときに <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.RemoveCommandFilter%2A> メソッドを呼び出して、これらのコマンドが渡されないようにします。

  処理する必要があるコマンドは、提供されているサービスによって異なります。 詳細については、 [言語サービス フィルターの重要なコマンド](../../extensibility/internals/important-commands-for-language-service-filters.md)」を参照してください。

  > [!NOTE]
  > <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> インターフェイスは、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスと同じオブジェクトに実装する必要があります。

- ステートメント入力候補

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> インターフェイスを実装します。

  ステートメント入力候補コマンド (つまり、<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>) をサポートし、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> インターフェイスの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> メソッドを呼び出して、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> インターフェイスを渡します。 詳細については、「[従来の言語サービスでのステートメント入力候補](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)」を参照してください。

- メソッドのヒント

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> インターフェイスを実装して、メソッドのヒント ウィンドウにデータを提供します。

  テキスト ビュー フィルターをインストールして、コマンドを適切に処理し、メソッド データ ヒント ウィンドウを表示するタイミングがわかるようにします。 詳細については、「[従来の言語サービスのパラメーター ヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)」をご覧ください。

- エラー マーカー

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> インターフェイスを実装します。

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> インターフェイスを実装するエラー マーカー オブジェクトを作成し、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> メソッドを呼び出して、エラー マーカー オブジェクトの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> インターフェイスを渡します。

  通常、各エラー マーカーでは、[タスク一覧] ウィンドウの項目を管理します。

- タスク一覧の項目

  <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskItem> インターフェイスを提供するタスク項目クラスを実装します。

  <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider> インターフェイスと <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2> インターフェイスを提供するタスク プロバイダー クラスを実装します。

  <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumTaskItems> インターフェイスを提供するタスク列挙子クラスを実装します。

  タスク プロバイダーをタスク一覧の <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RegisterTaskProvider%2A> メソッドに登録します。

  サービス GUID <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> で言語サービスのサービス プロバイダーを呼び出すことによって、<xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> インターフェイスを取得します。

  新規または更新されたタスクがある場合は、タスク項目オブジェクトを作成し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> インターフェイスの <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RefreshTasks%2A> メソッドを呼び出します。

- コメント タスク項目

  コメント タスク トークンを取得するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo> インターフェイスと <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens> インターフェイスを使用します。

  <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> サービスから <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo> インターフェイスを取得します。

  <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo.EnumTokens%2A> メソッドから <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens> インターフェイスを取得します。

  <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskListEvents> インターフェイスを実装して、トークン一覧の変更をリッスンします。

- アウトライン

  アウトラインのサポートにはいくつかのオプションがあります。 たとえば、 **[定義に縮小]** コマンドをサポートしたり、エディター制御のアウトライン領域を指定したり、クライアント制御領域をサポートしたりできます。 詳細については、「[方法: 従来の言語サービスでのアウトラインの拡張サポートの提供](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)」を参照してください。

- 言語サービスの登録

  言語サービスを登録する方法の詳細については、[従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service2.md) に関するページおよび「[VSPackage を管理する](../../extensibility/managing-vspackages.md)」を参照してください。

- 状況依存ヘルプ

  次のいずれかの方法で、エディターにコンテキストを提供します。

  - <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> インターフェイスを実装して、テキスト マーカーのコンテキストを提供します。

  - <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> インターフェイスを実装して、すべてのユーザー コンテキストを提供します。

## <a name="see-also"></a>関連項目
- [従来の言語サービスを開発する](../../extensibility/internals/developing-a-legacy-language-service.md)
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
