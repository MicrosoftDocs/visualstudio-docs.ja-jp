---
title: '&lt;customHostSpecified&gt; 要素 (Visual Studio での Office 開発)'
description: customHostSpecified 要素により、このソリューションがスタンドアロン アプリケーションではないことがどのように示されるか説明します。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <customHostSpecified> element
- <customHostSpecified> element
- customHostSpecified element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ba5ce54e862862c1e6750c78416fec4d5cf51cdd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99849984"
---
# <a name="ltcustomhostspecifiedgt-element-office-development-in-visual-studio"></a>&lt;customHostSpecified&gt; 要素 (Visual Studio での Office 開発)
  `customHostSpecified` 要素により、このソリューションがスタンドアロン アプリケーションではないことが示されます。 Office ソリューションには、Microsoft Office アプリケーション内でホストされるコンポーネントが含まれています。

## <a name="syntax"></a>構文

```xml
<customHostSpecified />
```

## <a name="elements-and-attributes"></a>要素と属性
 Office ソリューションには `customHostSpecified` 要素が必要です。 この要素は `co.v1` 名前空間に含まれており、カスタム ホストの内部に配置され、スタンドアロン アプリケーションではないコンポーネントがこの配置に含まれていることを指定します。

 この要素は、アプリケーション マニフェスト内の最初の `<entrypoint>` 要素の子です。 その `<entrypoint>` 要素内に他の子要素はなく、ある場合は、[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] によりインストール時に検証エラーが発生します。

 この要素には、属性も子要素もありません。

## <a name="example"></a>例
 次のコード例は、Office ソリューションに対するアプリケーション マニフェストの `customHostSpecified` 要素を示しています。 このコード例は、「[Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」に記載されている例から一部を抜粋したものです。

```xml
<entryPoint>
    <co.v1:customHostSpecified />
</entryPoint>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューション用配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)