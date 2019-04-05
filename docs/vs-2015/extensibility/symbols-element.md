---
title: 要素のシンボル |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- Symbols element (VSCT XML schema)
- VSCT XML schema elements, Symbols
ms.assetid: 1cda43d8-42a5-4b1b-a3c8-cf0401c3202f
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c8d28d225bd3a8d5c105bf54b9c63574002aed15
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58975691"
---
# <a name="symbols-element"></a>Symbols 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Guid およびその他の VSCT 要素で使用される Id を定義します。 アンマネージ コードは、この情報通常は、ヘッダー ファイルで指定されている[Extern 要素](../extensibility/extern-element.md)します。 マネージ コードがこの情報を定義するシンボルの要素の子要素。  
  
 既存の .cto ファイルから .vsct ファイルを作成する場合、シンボルがシンボル要素の子として生成されます。 詳細については、「[方法 :作成します。既存の Vsct ファイルです。Cto ファイル](../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file.md)します。  
  
 Symbols 要素と混同しないで、[定義要素](../extensibility/define-element.md)、プリプロセッサによって使用される名前と値のペアを定義します。  
  
## <a name="syntax"></a>構文  
  
```  
<Symbols>  
  <GuidSymbol>... </GuidSymbol>  
  <GuidSymbol>... </GuidSymbol>  
</Symbols>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|なし||  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|GuidSymbol|GUID 記号を定義します。 GuidSymbol が 2 つの必須属性: 名前と値。 名前は、シンボルの名前と値が文字列として GUID の値。<br /><br /> 例:\<GuidSymbol 名"guidVsPackage1Pkg"の値を = ="{c5f54698-101a-4846-84d3-dc748f9cd848}"/>|  
|IDSymbol|シンボルを定義します。 IDSymbol が 2 つの必須属性: 名前と値。 名前は、シンボルの名前と値が文字列としての記号の値。<br /><br /> 例:\<IDSymbol 名"MyMenuGroup"の値を = ="0x1020"/>|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[CommandTable 要素](../extensibility/commandtable-element.md)|.Vsct ファイルのルート要素。|  
  
## <a name="example"></a>例  
  
```  
<Symbols>  
  <GuidSymbol name="guidVsPackage1Pkg" value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />  
  <GuidSymbol name="guidVsPackage1CmdSet" value="{cb9dfd7f-2fcc-4a3e-aae8-f7fe30b1cfac}">  
    <IDSymbol name="MyMenuGroup" value="0x1020" />  
    <IDSymbol name="cmdidMyCommand" value="0x0100" />  
    <IDSymbol name="cmdidMyTool" value="0x0101" />  
  </GuidSymbol>  
</Symbols>  
```  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
