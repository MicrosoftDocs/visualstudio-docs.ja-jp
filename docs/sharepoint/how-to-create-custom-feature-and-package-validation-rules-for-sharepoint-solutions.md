---
title: SharePoint ソリューションの機能とパッケージの検証を作成する
titleSuffix: ''
description: Visual Studio によって生成されたソリューション パッケージを検証するか、または機能全体を検証するためのカスタム検証規則を作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
- SharePoint development in Visual Studio, validation rules
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ee6b27b92f1c79bfda95ba3d6dce7dbdce4a6fac
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216567"
---
# <a name="create-feature-and-package-validations-for-sharepoint-solutions"></a>SharePoint ソリューションの機能とパッケージの検証を作成する

  Visual Studio によって生成されたソリューション パッケージを検証するためのカスタム検証規則を作成できます。 **パッケージング エクスプローラー** でパッケージまたは機能のコンテキスト メニューから **[検証]** を選択することによって、機能またはパッケージ全体に対する完全な検証を実行できます。 部分検証は、プロジェクトに新しい SharePoint プロジェクト項目または機能を追加するときに、そのパッケージまたは機能が有効な状態になるかどうかを判定するために実行されます。

### <a name="to-create-a-custom-package-validation-rule"></a>カスタム パッケージ検証規則を作成するには

1. クラス ライブラリ プロジェクトを作成します。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. 次のいずれかのインターフェイスを実装するクラスを作成します。

    - パッケージ検証規則を作成するには、<xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule> インターフェイスを実装します。

    - 機能検証規則を作成するには、<xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule> インターフェイスを実装します。

4. <xref:System.ComponentModel.Composition.ExportAttribute> をクラスに追加します。 この属性を使用すると、Visual Studio で検証規則を検出して読み込むことができます。 属性コンストラクターに <xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule> または <xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule> 型を渡します。

## <a name="example"></a>例
 次のコード例は、カスタム機能検証規則を作成する方法を示しています。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/featurevalidation/extension/customvalidationrule.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/featurevalidation/extension/customfeaturevalidationrule.cs" id="Snippet1":::

## <a name="compile-the-code"></a>コードのコンパイル
 この例には、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint.

- System.ComponentModel.Composition.

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、その拡張機能で配布するアセンブリとその他のすべてのファイル用の [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint のパッケージ化と配置を拡張する](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
