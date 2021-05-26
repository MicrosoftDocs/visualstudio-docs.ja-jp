---
title: Visual Studio のワークスペースと言語サービス | Microsoft Docs
description: フォルダーを開くのユーザーがソリューションやプロジェクトを操作するときに使用するものと同じ高度な言語機能を備えた、言語サービスを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 815cfb9e17fed38b519719010acd997f7fdc5242
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877040"
---
# <a name="workspaces-and-language-services"></a>ワークスペースと言語サービス

言語サービスは、[フォルダーを開く](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)のユーザーに、ソリューションやプロジェクトを操作するときに使用するものと同じ高度な言語機能を提供できます。 言語サービスは、開いているドキュメントのファイル名拡張子またはコンテンツに基づいて自己アクティブ化することができます。ただし、この "緩いファイル" 言語サービスは構文の強調表示に限定されます。 ソース コードを編集または確認するときに、より高度なエクスペリエンスを提供するには、追加情報が必要です。 各言語サービスには、ドキュメントのこの追加コンテキスト データを使用して初期化するための独自 API が用意されています。 通常、これはプロジェクト システムによって管理され、言語サービスとビルド システムの両方に密結合されます。

## <a name="initialization"></a>初期化

[ワークスペース](workspaces.md)では、言語サービスはその言語サービスのみに特化し、ビルドの作成については何も認識しない <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> 拡張ポイントによって初期化されます。 このようにして、言語サービスの所有者は、ビルド中にコンパイラを実行するためのフォルダーやファイル (たとえば、MSBuild やメイクファイルなど) 内のパターンの数に関係なく、1 つのフォルダーを開くの拡張機能を維持できます。 ファイル コンテキストが作成されたファイルがディスク上で変更され、ファイル コンテキストが更新されると、更新されたファイル コンテキストのセットが言語サービス プロバイダーに通知されます。 言語サービス プロバイダーは、そのモデルを更新できます。

エディターでドキュメントが開かれている場合、Visual Studio では、一致するファイル コンテキスト プロバイダーが見つかるファイル コンテキストの種類を必要とする言語サービス プロバイダーのみが考慮されます。 次に、`ILanguageServiceProvider.InitializeAsync` を使用して、一致するプロバイダーのファイル コンテキストを、選択した言語サービス プロバイダーに渡します。 言語サービス プロバイダーがそのファイル コンテキスト データを使用して行うことは、言語サービス プロバイダーの実装の詳細ですが、想定されるユーザー エクスペリエンスは、開いているドキュメントに対してより高度な言語サービスになります。

## <a name="using-ilanguageserviceprovider"></a>ILanguageServiceProvider の使用

言語サービスは、言語サーバーの export 属性の `SupportedContextTypes` 値に一致する `ContextType` を使用してファイル コンテキストが作成されたときに、通知を受けます。

言語サービスをサポートするには、拡張機能に次のものが必要です。

- 一意な `Guid`。 これは、`SupportedContextTypes` 属性引数および `FileContext` オブジェクトで使用されます。
- 言語ファイル コンテキスト
  - プロバイダー ファクトリ
    - `SupportedContextTypes` の `ExportFileContextProviderAttribute` 属性が上記の一意に生成された `Guid`
    - `IWorkspaceProviderFactory<IFileContextProvider>` を実装します
  - `IFileContextProvider.GetContextsForFileAsync` のプロバイダー実装
    - `contextType` コンストラクター引数を使用して、一意に生成された `Guid` として新しい `FileContext` を構築します
    - `FileContext` の `Context` プロパティを使用して、`ILanguageServiceProvider` に追加のデータを渡します
- 言語サービス
  - プロバイダー ファクトリ
    - `SupportedContextTypes` の `ExportLanguageServiceProvider` 属性が上記の一意に生成された `Guid`
    - `IWorkspaceProviderFactory<ILanguageServiceProvider>` を実装します
  - プロバイダー
    - `ILanguageServiceProvider` を実装します
    - ファイルを開いたときに、指定された引数の言語サービスを有効にするために `ILanguageServiceProvider.InitializeAsync` を使用します
    - ファイルを閉じたときに、指定された引数の言語サービスを無効にするために `ILanguageServiceProvider.UninitializeAsync` を使用します

>[!WARNING]
>`ILanguageServiceProvider` メソッドは、メイン スレッドのワークスペースによって呼び出されることがあります。 UI の遅延が発生しないように、別のスレッドで作業をスケジュールすることを検討してください。

## <a name="language-server-protocol"></a>言語サーバー プロトコル

`Microsoft.VisualStudio.Workspace.*` API は、フォルダーを開くで言語サービスを有効にする唯一の方法ではありません。 もう 1 つのオプションは、言語サーバーを使用することです。 詳細については、[言語サーバー プロトコル](language-server-protocol.md)に関する説明を参照してください。

## <a name="related-interfaces"></a>関連インターフェイス

- <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> は、ファイルの種類が一致するファイルが編集のために開かれるか、閉じられるときに呼び出されます。

## <a name="next-steps"></a>次のステップ

* [ワークスペース ビルド](workspace-build.md) -フォルダーを開くは、MSBuild やメイクファイルなどのビルド システムをサポートします。