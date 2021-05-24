---
description: vstov4 名前空間の document 要素には、ドキュメント レベルのカスタマイズに関するカスタマイズ固有の情報が格納されます。
title: '&lt;document&gt; 要素 (Visual Studio での Office 開発)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document element
- application manifests [Office development in Visual Studio], <document> element
- <document> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3563169bd9b567cd974248bf4185cb9bc8a7b022
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221042"
---
# <a name="ltdocumentgt-element-office-development-in-visual-studio"></a>&lt;document&gt; 要素 (Visual Studio での Office 開発)
  `vstov4` 名前空間の `document` 要素には、ドキュメント レベルのカスタマイズに関するカスタマイズ固有の情報が格納されます。

## <a name="syntax"></a>構文

```xml
<document solutionId />
```

## <a name="elements-and-attributes"></a>要素と属性
 ドキュメント レベルのカスタマイズの場合にのみ必須。 `document` 要素は `vstov4` 名前空間に属します。 `document` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`solutionId`|必須。 ドキュメント レベルのソリューションを一意に識別するために Visual Studio Tools for Office ランタイムによって使用される GUID。 この値は、_AssemblyLocation カスタム ドキュメント プロパティとして格納されます。 詳細については、「[カスタム ドキュメントのプロパティの概要](../vsto/custom-document-properties-overview.md)」を参照してください。|

 `document` に子要素はありません。

## <a name="document-level-customization-example"></a>ドキュメント レベルのカスタマイズの例

### <a name="description"></a>説明
 次のコード例は、[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] を使用して配置されるドキュメント レベルの Office ソリューションでの `document` 要素を示したものです。 このコード例は、「[Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」で提供されている大きな例の一部です。

### <a name="code"></a>コード

```xml
<vstov4:document
  solutionId="73e" />
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューション用配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
