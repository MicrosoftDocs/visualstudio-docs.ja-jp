---
description: vstov4 名前空間の friendlyName 要素には、インストールしたプロフラムの一覧に表示される名前を格納します。
title: '&lt;friendlyName&gt; 要素 (Visual Studio での Office 開発)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <friendlyName> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: adcf46a2c232176026181283549c0c59fc713603
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223447"
---
# <a name="ltfriendlynamegt-element-office-development-in-visual-studio"></a>&lt;friendlyName&gt; 要素 (Visual Studio での Office 開発)
  `friendlyName` 名前空間の `vstov4` 要素には、インストールしたプロフラムの一覧に表示される名前を格納します。

## <a name="syntax"></a>構文

```xml
<friendlyName>
</friendlyName>
```

## <a name="elements-and-attributes"></a>要素と属性
 `friendlyName` 要素は `vstov4` 名前空間に属します。 この値は、コンピューターにインストールされているプログラムの一覧と、Microsoft Office アプリケーションの COM VSTO アドイン ダイアログ ボックスに表示されます。

 `friendlyName` 要素には、属性も子要素もありません。

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="description"></a>説明
 次のコード例は、 `friendlyName` を使用して配置されるアプリケーションレベルのソリューションの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、「[Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」に記載されている例から一部を抜粋したものです。

### <a name="code"></a>コード

```xml
<vstov4:friendlyName>
  ContosoOutlookAddIn
</vstov4:friendlyName>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューション用配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
