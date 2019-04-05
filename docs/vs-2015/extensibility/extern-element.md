---
title: Extern 要素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- Extern
helpviewer_keywords:
- VSCT XML schema elements, Extern
- Extern element (VSCT XML schema)
ms.assetid: db6c3ddd-a1ba-450a-897a-bb568a5377fc
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 17477b7eb60aa332f6910019e28f4c53aa31ebf1
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58976269"
---
# <a name="extern-element"></a>Extern 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Extern 要素は、コンパイル時に、.vsct ファイルとマージする外部ヘッダー (.h) ファイルを参照します。 VSCT コンパイラに指定されたかによって参照されるインクルード パスにファイルをマージする必要があります、 [Include 要素](../extensibility/include-element.md)します。 ファイルには、他の .vsct ファイルまたは C++ ヘッダー ファイルがあります。  
  
 フォームのヘッダー ファイル内の定義がある必要があります"# [Value] の [記号] define"値は、以前に定義されている場合、別のシンボル可能性があります。 コマンドの項目の条件付きステートメントでは、定義を使用することがあります。 実際に使用される任意のシンボルは破棄されます。  
  
 CommandTable 要素  
Extern 要素  
  
## <a name="syntax"></a>構文  
  
```  
<Extern href="stdidcmd.h" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|href|必須。 ヘッダー ファイルへのパス:<br /><br /> href="stdidcmd.h"|  
|条件|任意。 参照してください[条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)します。|  
|language|省略可能です。 すべての既定の言語[\<文字列 >](../extensibility/strings-element.md)コマンド テーブル内の要素。<br /><br /> language="en-us"|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|なし。|なし。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[CommandTable 要素](../extensibility/commandtable-element.md)|すべてのコマンドを表す要素の定義: メニュー項目、メニューのツールバー、およびコンボ ボックスは、-、IDE に VSPackage を提供します。|  
  
## <a name="example"></a>例  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-  
  18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <Extern href="C:\VSCore\vscommon\inc\vsshlids.h"/>  
    …  
  <Commands package="guidMyPackage">  
</CommandTable>  
```  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio コマンド テーブル (します。Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [Vspackage がユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
