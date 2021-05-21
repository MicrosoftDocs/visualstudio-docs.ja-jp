---
title: '&lt;postActions&gt; 要素 (Office 開発)'
description: vstav3 名前空間の postActions 要素には、Office ソリューションのインストール後に実行される配置後アクションが記述されているすべての postAction 要素が格納されます。
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <postActions> element
- postActions element
- <postActions> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5c4a66e270cd446996884262d380df0f7384f54f
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102470041"
---
# <a name="ltpostactionsgt-element-office-development"></a>&lt;postActions&gt; 要素 (Office 開発)
  `postActions` 名前空間の `vstav3` の要素には、Office ソリューションのインストール後に実行する配置後アクションを説明する `postAction` 要素がすべて含まれています。

## <a name="syntax"></a>構文

```xml
<postActions>
  <postAction>
    <entryPoint>
    </entryPoint>
    <postActionData>
    </postActionData>
  </postAction>
</postActions>
```

## <a name="elements-and-attributes"></a>要素と属性
 `postActions` 要素は省略可能であり、 `vstav3` 名前空間にあります。 アプリケーション マニフェストで定義された `postActions` 要素が 1 つだけあります。

 `postActions` 要素に属性はありません。

 `postActions` には、次の要素があります。

### <a name="postaction"></a>postAction
 省略可能。 `vstav3` 名前空間での `postAction` 要素の役割は、「[&#60;postAction&#62; 要素 &#40;Visual Studio での Office 開発&#41;](../vsto/postaction-element-office-development-in-visual-studio.md)」で定義されています。

## <a name="post-deployment-action-example"></a>配置後アクションの例

### <a name="description"></a>説明
 次のコード例は、 `postActions` を使用して配置する Office ソリューションに対するアプリケーション マニフェストの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、「[Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」で提供されている大きな例の一部です。

### <a name="code"></a>コード

```xml
<vstav3:postActions>
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
</vstav3:postActions>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューション用配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
