---
title: 要素をグループ化 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Groups
- Groups element (VSCT XML schema)
ms.assetid: 69faee18-cbf4-470a-b952-c1919c583df8
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 35528f694cf76c1971e07023125706c962e77fe2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62911821"
---
# <a name="group-element"></a>Group 要素
VSPackage のコマンド グループを定義します。

## <a name="syntax"></a>構文

```xml
<Group guid="guidMyCommandSet" id="MyGroup" priority="0x101">
  <Parent>... </Parent>
</Group>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 コマンド id を GUID と ID の GUID です。|
|ID|必須。 コマンド id を GUID と ID の ID。|
|priority|任意。 優先度を示す数値。|
|条件|任意。 参照してください[条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)します。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|親|省略可能です。 ボタンの親要素。|
|注釈|省略可能なコメント。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Groups 要素](../extensibility/groups-element.md)|VSPackage のコマンド グループを定義するエントリが含まれています。|

## <a name="example"></a>例

```xml
<Group guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">
  <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_MAINMENU"/>
</Group>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)