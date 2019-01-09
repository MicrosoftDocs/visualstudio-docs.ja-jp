---
title: XmlPoke タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- XmlPoke task [MSBuild]
- MSBuild, XmlPoke task
ms.assetid: 6ba1953c-be3b-4df8-8561-e133408f8270
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6a12991a8ea3de4348ce87686feadd7bc7681968
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53934240"
---
# <a name="xmlpoke-task"></a>XmlPoke タスク

XML ファイルに XPath クエリで指定された値を設定します。

## <a name="parameters"></a>パラメーター

 `XmlPoke` タスクのパラメーターの説明を次の表に示します。
  
|パラメーター|説明|
|---------------|-----------------|
|`Namespaces`|省略可能な `String` 型のパラメーターです。<br /><br /> XPath クエリ プレフィックスの名前空間を指定します。 `Namespaces` は、属性 `Prefix` と `Uri` を持つ `Namespace` 要素で構成される XML スニペットです。 属性 `Prefix` では、`Uri` 属性で指定された名前空間に関連付けるプレフィックスを指定します。 空の `Prefix` は使用しないでください。|
|`Query`|省略可能な `String` 型のパラメーターです。<br /><br /> XPath クエリを指定します。|
|`Value`|必須の <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> 指定されたパスに挿入する値を指定します。|
|`XmlInputPath`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> XML 入力をファイル パスとして指定します。|

## <a name="remarks"></a>コメント

 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例

以下に、変更する sample.xml を示します。

```xml
<Package xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
         xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" >
<Identity Name="Sample.Product " Publisher="CN=1234" Version="1.0.0.0" />
<mp:PhoneIdentity PhoneProductId="456" PhonePublisherId="0" />
</Package>
```

この例では、`/Package/mp:PhoneIdentity/PhonePublisherId` を変更する場合、以下を使用します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Namespace>
        <Namespace Prefix="dn" Uri="http://schemas.microsoft.com/appx/manifest/foundation/windows10" />
        <Namespace Prefix="mp" Uri="http://schemas.microsoft.com/appx/2014/phone/manifest" />
        <Namespace Prefix="uap" Uri="http://schemas.microsoft.com/appx/manifest/uap/windows10" />
    </Namespace>
</PropertyGroup>

<Target Name="Poke">
  <XmlPoke
    XmlInputPath="Sample.xml"
    Value="MyId"
    Query="/dn:Package/mp:PhoneIdentity/@PhoneProductId"
    Namespaces="$(Namespace)"/>
</Target>
</Project>
```

ここでは、既定の名前空間の人為的な名前空間プレフィックスとして `dn` が使用されます。

## <a name="see-also"></a>関連項目

 [タスク](../msbuild/msbuild-tasks.md)   
 [タスク リファレンス](../msbuild/msbuild-task-reference.md)
