---
title: サポートされているコード変更 (C# および Visual Basic) | Microsoft Docs
ms.date: 10/11/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [C#], supported code changes
- Edit and Continue [Visual Basic], supported code changes
ms.assetid: c7a48ea9-5a7f-4328-a9d7-f0e76fac399d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 44881035da14483c3ddf1f4c48cb3957a1ce8b50
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72729089"
---
# <a name="supported-code-changes-c-and-visual-basic"></a>サポートされているコード変更 (C# および Visual Basic)
エディット コンティニュでは、メソッドの本体内で行ったほとんどの種類のコード変更を処理できます。 しかし、メソッドの本体外で行った変更の大部分やメソッドの本体内で行った一部の変更は、デバッグ時に適用できません。 このようなサポートされていない変更を適用するには、デバッグを停止し、新しいバージョンのコードを再起動する必要があります。

## <a name="supported-changes-to-code"></a>コードに対するサポートされている変更

次の表に、デバッグ セッション中にセッションの再起動なしで C# コードと Visual Basic コードに対して実行できる変更を示します。

|言語要素/機能|サポートされている編集操作|制限事項|
|-|-|-|
|型|メソッド、フィールド、コンス トラクター、他を追加します。|[はい](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|
|Iterators|追加または変更します。|いいえ|
|非同期/待機式|追加または変更します。|[はい](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|
|動的オブジェクト|追加または変更します。|いいえ|
|ラムダ式|追加または変更します。|[はい](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|
|LINQ 式|追加または変更します。|[ラムダ式と同じ](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|

> [!NOTE]
> エディット コンティニュでは、通常、文字列補間や null 条件演算子などの新しい言語機能がサポートされます。 最新の情報については、[EnC でサポートされている編集](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)に関するページを参照してください。

## <a name="unsupported-changes-to-code"></a>コードに対するサポートされていない変更
 デバッグ セッション中、C# コードと Visual Basic コードに次の変更を適用することはできません。

- 現在のステートメントまたはその他のアクティブ ステートメントに対する変更。

     アクティブ ステートメントには、現在のステートメントを取得するために呼び出される、呼び出し履歴上の関数内に存在するすべてのステートメントが含まれます。

     ソース ウィンドウ内では、現在のステートメントは黄色の背景で示されます。 その他のアクティブ ステートメント (読み取り専用) は、網かけの背景で示されます。 これらの既定の色は、 **[オプション]** ダイアログ ボックスで変更できます。

- 次の表に、コードに対するサポートされていない変更を言語要素別に示します。

|言語要素/機能|サポートされていない編集操作|
|-|-|
|すべてのコード要素|名前の変更|
|名前空間|追加|
|名前空間、型、メンバー|削除|
|ジェネリック|追加または変更します。|
|インターフェイス|変更|
|型|抽象または仮想メンバーを追加し、オーバーライドを追加する ([詳細](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)を参照)|
|型|デストラクターを追加します。|
|メンバー|埋め込まれた相互運用機能型を参照するメンバーを変更する|
|メンバー|実行中のコードによって既にアクセスされた後で静的メンバーを変更する|
|メンバー (Visual Basic)|On Error または Resume ステートメントを使用してメンバーを変更する|
|メンバー (Visual Basic)|Aggregate、Group By、Simple Join、または Group Join LINQ クエリ句を含むメンバーを変更する|
|メソッド|シグネチャを変更する|
|メソッド|メソッド本体を追加することで、抽象メソッドを非抽象にする|
|メソッド|メソッド本体を削除する|
|属性|追加または変更します。|
|イベントまたはプロパティ|型パラメーター、基本型、デリゲート型、または戻り値の型を変更する |
|演算子またはインデクサー|型パラメーター、基本型、デリゲート型、または戻り値の型を変更する |
|catch ブロック|アクティブ ステートメントが含まれているときに変更する|
|try-catch-finally ブロック|アクティブ ステートメントが含まれているときに変更する|
|using ステートメント|追加|
|非同期メソッド/ラムダ|.NET Framework 4 以下を対象とするプロジェクトで非同期メソッド/ラムダを変更する ([詳細](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)を参照)|
|Iterators|.NET Framework 4 以下を対象とするプロジェクトで反復子を変更する ([詳細](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)を参照)|

## <a name="unsafe-code"></a>アンセーフ コード
 アンセーフ コードを変更する場合、セーフ コードを変更するときと同じ制限に加えて、もう 1 つ追加の制限が適用されます。エディット コンティニュでは、`stackalloc` 演算子を含むメソッド内に存在するアンセーフ コードの変更はサポートされていません。

## <a name="unsupported-app-scenarios"></a>サポートされていないアプリ シナリオ

サポートされていないアプリおよびプラットフォームとしては、ASP.NET 5、Silverlight 5、Windows 8.1 などがあります。

> [!NOTE]
> サポートされていないアプリには、Windows 10 の UWP および .NET Framework 4.6 デスクトップ以降のバージョン (.NET Framework はデスクトップ バージョンのみ) を対象とする x86 および x64 アプリが含まれています。

## <a name="unsupported-scenarios"></a>サポートされていないシナリオ
 次のデバッグ シナリオでは、エディット コンティニュを使用できません。

- 混合モードでの (ネイティブ/マネージ) デバッグ

- SQL デバッグ

- ワトソン博士のダンプのデバッグ。

- 埋め込まれたランタイム アプリケーションのデバッグ

- **[デバッグ]** メニューから **[開始]** を選択してアプリケーションを実行する代わりに、プロセスへのアタッチ ( **[デバッグ] > [アタッチ先]** ) を使用してアプリをデバッグする

- 最適化されたコードのデバッグ

- ビルド エラーによって新しいバージョンのビルドが失敗した後の旧バージョンのデバッグ

## <a name="see-also"></a>関連項目
- [エディット コンティニュ (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)
- [方法: エディット コンティニュを使用する (C#)](../debugger/how-to-use-edit-and-continue-csharp.md)