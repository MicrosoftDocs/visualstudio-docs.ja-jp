---
title: UsedCommand 要素 | Microsoft Docs
description: UsedCommand 要素により、VSPackage から別の .vsct ファイルで定義されているコマンドにアクセスできるようになります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 99cd05d3-644a-42ff-b289-8458cd1b20c0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9d120353b9d6191bfcaae38151eb970ab1071b99
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903048"
---
# <a name="usedcommand-element"></a>UsedCommand 要素
VSPackage から別の .vsct ファイルで定義されているコマンドにアクセスできるようになります。 たとえば、VSPackage が [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] シェルによって定義されている標準の **Copy** コマンドを使用する場合、コマンドを再実装せずにメニューまたはツール バーに追加できます。

## <a name="syntax"></a>構文

```
<UsedCommand guid="guidMyCommandGroup" id="MyCommand" />
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 コマンドを識別する GUID ID ペアの GUID。|
|id|必須。 コマンドを識別する GUID ID ペアの ID。|
|条件|省略可能。 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)に関するページを参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|なし||

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[UsedCommands 要素](../extensibility/usedcommands-element.md)|UsedCommand 要素とその他の UsedCommands グループをグループ化します。|

## <a name="remarks"></a>解説
 `<UsedCommands>` 要素にコマンドを追加することにより、VSPackage がコマンドを必要としていることが VSPackage から [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 環境に通知されます。 Visual Studio のすべてのバージョンと構成に含まれていない可能性があるパッケージで必要なすべてのコマンドに対して、`<UsedCommand>` 要素を追加する必要があります。 たとえば、パッケージから Visual C++ に固有のコマンドが呼び出されると、コマンドに `<UsedCommand>` 要素を含めない限り、Visual Web Developer のユーザーはこのコマンドを使用できません。

## <a name="example"></a>例

```
<UsedCommands>
  <UsedCommand guid="guidVSStd97" id="cmdidCut"/>
  <UsedCommand guid="guidVSStd97" id="cmdidCopy"/>
  <UsedCommand guid="guidVSStd97" id="cmdidPaste"/>
</UsedCommands>
```

## <a name="see-also"></a>関連項目
- [UsedCommands 要素](../extensibility/usedcommands-element.md)
- [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
