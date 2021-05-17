---
title: '&lt;customErrorReporting&gt; 要素 (ClickOnce 配置) | Microsoft Docs'
description: customErrorReporting 要素では、例外スタックを示すエラー ダイアログ ボックスの代わりに、いつエラーが発生したかを表示する URI を指定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <customErrorReporting> element [ClickOnce deployment manifest]
ms.assetid: 7d31816e-c692-46b5-9cc9-753284b3bcda
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b168b3bcb90ae758609698de306928eb7e13d909
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888486"
---
# <a name="ltcustomerrorreportinggt-element-clickonce-deployment"></a>&lt;customErrorReporting&gt; 要素 (ClickOnce 配置)
エラー発生時に表示する URI を指定します。

## <a name="syntax"></a>構文

```xml
<customErrorReporting
   uri
/>
```

## <a name="remarks"></a>解説
 この要素は省略可能です。 これがないと、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では例外スタックを示すエラー ダイアログ ボックスが表示されます。 `customErrorReporting` 要素が存在する場合は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] により、`uri` パラメーターによって指定された URI が代わりに表示されます。 ターゲット URI には、パラメーターとして、外部例外クラス、内部例外クラス、内部例外メッセージが含められます。

 この要素を使用して、アプリケーションにエラー報告機能を追加します。 生成される URI にはエラーの種類に関する情報が含まれているため、Web サイトでは、その情報を解析して、適切なトラブルシューティング画面などを表示することができます。

## <a name="example"></a>例
 次のスニペットには、`customErrorReporting` 要素と、それによって生成される可能性のある、生成後の URI が一緒と示されています。

```xml
<customErrorReporting uri=http://www.contoso.com/applications/error.asp />

Example Generated Error:
http://www.contoso.com/applications/error.asp? outer=System.Deployment.Application.InvalidDeploymentException&&inner=System.Deployment.Application.InvalidDeploymentException&&msg=The%20application%20manifest%20is%20signed,%20but%20the%20deployment%20manifest%20is%20unsigned.%20Both%20manifests%20must%20be%20either%20signed%20or%20unsigned.
```

## <a name="see-also"></a>関連項目
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)