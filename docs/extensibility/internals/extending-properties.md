---
title: プロパティの拡張 | Microsoft Docs
description: Visual Studio のプロパティ ウィンドウでプロパティの一覧を拡張するために実装と呼び出しが必要なインターフェイスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, providing support
ms.assetid: 68e2cbd4-861c-453f-8c9f-4ab6afc80e67
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3b1006f74cd2de03b4fe74e090d7ffcd1c921e5d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069648"
---
# <a name="extend-properties"></a>プロパティの拡張
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の **[プロパティ]** ウィンドウは、COM および COM+ コンポーネントのユニバーサル プロパティ ブラウザーであり、すべての [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 製品がサポートされます。 **[プロパティ]** ウィンドウでは、`ITypeInfo` 型情報と COM+ メタデータを使用して、統合開発環境 (IDE) の他のウィンドウで現在選択されているオブジェクトのデザイン時プロパティを一覧表示します。

 **[プロパティ]** ウィンドウは、キーボードの **F4** キーを押すか、 **[表示]** メニューの **[プロパティ ウィンドウ]** を選択して開くことができます。このウィンドウを使用して、選択したオブジェクトについて構成非依存のデザイン時プロパティやイベントを表示および編集できます。 ソリューションおよびプロジェクトに関連付けられている構成依存のプロパティは、[[プロパティ ページ]](../../extensibility/internals/property-pages.md)に表示されます。 詳細については、「[構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)」を参照してください。

 ![プロパティ ウィンドウの概要](../../extensibility/internals/media/vspropertieswindow.png "vsPropertiesWindow") プロパティ ウィンドウ

 このセクションでは、**プロパティ** ウィンドウの個々の領域に関連する詳細情報と、ウィンドウにデータを読み込むために実装と呼び出しが必要なインターフェイスについて説明します。

## <a name="in-this-section"></a>このセクションの内容
- [プロパティ ウィンドウの概要](../../extensibility/internals/properties-window-overview.md)

 ツール ウィンドウとドキュメント ウィンドウを基準として、**プロパティ** ウィンドウの目的について説明します。

- [テンプレート ポリシーとプロパティ ウィンドウ](../../extensibility/internals/template-policy-and-the-properties-window.md)

 エンタープライズ テンプレート プロジェクト内にプロジェクトを含める方法と、そのエンタープライズ テンプレートプロジェクトでポリシーを適用する方法について説明します。

- [プロパティ ウィンドウのフィールドとインターフェイス](../../extensibility/internals/properties-window-fields-and-interfaces.md)

 **プロパティ** ウィンドウに表示する情報を決定する選択基準について説明します。

- [プロパティ ウィンドウのオブジェクト一覧](../../extensibility/internals/properties-window-object-list.md)

 **プロパティ** ウィンドウのオブジェクト一覧の目的と、この一覧の別のオブジェクトで呼び出しをトリガーするときに、新しいオブジェクトが選択されたことが通知される方法について説明します。

- [プロパティ ウィンドウのボタン](../../extensibility/internals/properties-window-buttons.md)

 **プロパティ** ウィンドウのツール バーに表示される 4 つの既定のボタンの目的について説明します。

- [プロパティ表示グリッド](../../extensibility/internals/properties-display-grid.md)

 プロパティ名とプロパティ値のフィールドがグリッドで表示される場所について説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクト タイプ](../../extensibility/internals/project-types.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE の構成要素としてのプロジェクトについて説明します。

- [コンパイルとビルド](../../ide/compiling-and-building-in-visual-studio.md)

 アプリケーションをビルドするときに、継続的にテストおよびデバッグするために [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プラットフォームを使用する方法について説明します。

- [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)

 `IDispatch` インターフェイスについて説明します。当初はオートメーションをサポートするために設計されましたが、オブジェクトのメソッドおよびプロパティに関する情報にアクセスしたり取得したりするための遅延バインディング機構を提供しています。

- [アプリケーション設定の管理 (.NET)](../../ide/managing-application-settings-dotnet.md)

 アプリケーション設定の概要について説明します。アプリケーション設定を使用すると、アプリケーションのコンパイル済みコードではなく外部構成ファイルにプロパティ値が格納されるようにアプリケーションを構成できます。

- [ソリューションおよびプロジェクト](../../ide/solutions-and-projects-in-visual-studio.md)

 ソリューションとプロジェクトを通じて、開発作業に必要な参照、データ接続、フォルダー、ファイルなどの項目を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で効率的に管理する方法について説明します。

- [Visual Studio の他の部分を拡張する](../../extensibility/extending-other-parts-of-visual-studio.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] サービスを使用して、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の他の部分に相当する UI 要素を作成する方法について説明します。
