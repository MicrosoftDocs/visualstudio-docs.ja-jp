---
title: '&lt;update&gt; 要素 (Visual Studio での Office 開発)'
description: Update 要素では、ソリューションで更新プログラムをチェックする間隔を指定します。
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- update element
- <update> element
- application manifests [Office development in Visual Studio], <update> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 59e7b21902c486bd78548cd79f2e79a5056042a5
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102468508"
---
# <a name="ltupdategt-element-office-development-in-visual-studio"></a>&lt;update&gt; 要素 (Visual Studio での Office 開発)
  `update` 要素では、ソリューションで更新プログラムをチェックする間隔を指定します。

## <a name="syntax"></a>構文

```xml
<update
  enabled>
  <expiration
    maximumAge
    unit
  />
</update>
```

## <a name="elements-and-attributes"></a>要素と属性
 `update` 要素は必須です。この要素は `vstav3` 名前空間にあります。

 `update` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`enabled`|必須。 enabled には次のいずれかの値を設定します。<br /><br /> -   **true** 更新プログラムを確認する場合。<br />-   **false** 更新プログラムをチェックしないようにする場合。|

 `update` 要素には、次の子要素があります。

### <a name="expiration"></a>expiration
 `expiration` 要素は必須です。この要素は `vstav3` 名前空間にあります。 この要素では、ソリューションで更新プログラムをチェックする間隔を指定します。

 `expiration` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`maximumAge`| 必須。 これは整数と等しくなるように設定します。|
|`unit`|必須。 `unit` には、次のいずれかの値を選択します。<br /><br /> -   **時間**<br />-   **日**<br />-   **週**|

## <a name="example-of-always-checking-for-updates"></a>常に更新プログラムを確認する例

### <a name="description"></a>説明
 次のコード例は、Office ソリューションで常に更新プログラムをチェックするように設定されている `update` 要素を示しています。

### <a name="code"></a>コード

```xml
<vstav3:update enabled="true" />
```

## <a name="example-of-setting-a-default-update-interval"></a>既定の更新間隔を設定する例

### <a name="description"></a>説明
 次のコード例は、Office ソリューションのアプリケーション マニフェストの `update` 要素を示しています。 このコード例は、「[Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」に記載されている例から一部を抜粋したものです。

### <a name="code"></a>コード

```xml
<vstav3:update enabled="true">
    <vstav3:expiration maximumAge="7" unit="days" />
</vstav3:update>
```

## <a name="see-also"></a>関連項目

- [ClickOnce を使用して Office ソリューションを配置する](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューション用配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
