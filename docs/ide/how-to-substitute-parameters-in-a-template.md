---
title: プロジェクトと項目テンプレートに名前パラメーターを追加する
ms.date: 01/02/2018
ms.topic: conceptual
helpviewer_keywords:
- template parameters
- template parameters, substituting
- Visual Studio templates, using parameters
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 09d86c52fcd9ddce3c986e0bfa6c9c96f746c663
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656564"
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