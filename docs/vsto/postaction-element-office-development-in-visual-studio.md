---
title: '&lt;postAction&gt; 要素 (Visual Studio での Office 開発)'
description: vstav3 名前空間の postAction 要素には、Office ソリューションのインストール後に実行される配置後アクションに関連付けらえている entrypoint 要素とすべての postActionData 要素が格納されます。
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <postAction> element
- <postAction> element
- postAction element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 04f8c92c52aeee9f7f1dd5ab67b3dcef3a295474
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102470054"
---
# <a name="ltpostactiongt-element-office-development-in-visual-studio"></a>&lt;postAction&gt; 要素 (Visual Studio での Office 開発)
  `postAction` 名前空間の `vstav3` 要素には、配置後アクションに関連付ける `entrypoint` 要素とすべての `postActionData` 要素を格納します。これらの要素は、Office ソリューションのインストール後に実行されます。

## <a name="syntax"></a>構文

```xml
<postAction>
  <entryPoint>
  </entryPoint>
  <postActionData>
  </postActionData>
</postAction>
```

## <a name="elements-and-attributes"></a>要素と属性
 `postAction` 要素は省略可能であり、 `vstav3` 名前空間にあります。 アプリケーション マニフェストには、配置後アクションごとに `postAction` 要素を 1 つ定義します。

 `postAction` 要素に属性はありません。

 `postAction` には、次の要素があります。

### <a name="entrypoint"></a>entryPoint
 省略可能。 `vstav3` 名前空間での `entryPoint` 要素の役割は、「[&#60;entryPoints&#62; 要素 &#40;Visual Studio での Office 開発&#41;](../vsto/entrypoints-element-office-development-in-visual-studio.md)」で定義されています。

### <a name="postactiondata"></a>postActionData
 省略可能。 `vstav3` 名前空間での `postActionData` 要素の役割は、「[&#60;postActionData&#62; 要素 &#40;Visual Studio での Office 開発&#41;](../vsto/postactiondata-element-office-development-in-visual-studio.md)」で定義されています。

## <a name="post-deployment-action-example"></a>配置後アクションの例

### <a name="description"></a>説明
 次のコード例は、 `postAction` を使用して配置する Office ソリューションに対するアプリケーション マニフェストの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、「[Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」で提供されている大きな例の一部です。

### <a name="code"></a>コード

```xml
<vstav3:postAction>
  <vstav3:entryPoint
    class="PostDeploymentAction.PostDeploymentActionSample">
    <assemblyIdentity
      name="PostDeploymentAction"
      version="1.0.0.0"
      language="neutral"
      processorArchitecture="msil" />
  </vstav3:entryPoint>
  <vstav3:postActionData>
  </vstav3:postActionData>
</vstav3:postAction>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューション用配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
