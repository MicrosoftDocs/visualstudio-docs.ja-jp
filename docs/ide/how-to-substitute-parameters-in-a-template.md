---
title: プロジェクトと項目テンプレートに名前パラメーターを追加する
ms.date: 01/02/2018
ms.topic: conceptual
helpviewer_keywords:
- template parameters
- template parameters, substituting
- Visual Studio templates, using parameters
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: cf9a990be3f5e87180967a4f9f274ec79fbc357e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946883"
---
# <a name="how-to-substitute-parameters-in-a-template"></a>方法:テンプレート内のパラメーターを置き換える

テンプレート パラメーターを使うと、テンプレートからファイルを作成するときに、クラス名や名前空間などの識別子を置き換えることができます。 既存のテンプレートにテンプレート パラメーターを追加することも、テンプレート パラメーターで独自のテンプレートを作成することもできます。

テンプレート パラメーターは、$*parameter*$ という形式で記述します。 テンプレート パラメーターの完全な一覧については、「[テンプレート パラメーター](../ide/template-parameters.md)」を参照してください。

次のセクションでは、名前空間の名前を "安全なプロジェクト名" に置き換えるようにテンプレートを変更する方法を示します。

## <a name="example---namespace-name"></a>例 - 名前空間の名前

1. テンプレートの 1 つ以上のコード ファイルにパラメーターを挿入します。 次に例を示します。

    ```csharp
    namespace $safeprojectname$
    ```

1. テンプレートの *vstemplate* ファイルで、このファイルを含む `ProjectItem` 要素を検索します。

1. `ProjectItem` 要素の `ReplaceParameters` 属性を `true` に設定します。

    ```xml
    <ProjectItem ReplaceParameters="true">Class1.cs</ProjectItem>
    ```

## <a name="see-also"></a>関連項目

- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [ProjectItem 要素 (Visual Studio 項目テンプレート)](../extensibility/projectitem-element-visual-studio-item-templates.md)