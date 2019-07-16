---
title: 要素をコマンド |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- Commands
helpviewer_keywords:
- Commands element (VSCT XML schema)
- VSCT XML schema elements, Commands
ms.assetid: 47cf16a5-d78b-452e-86f6-b5893856dddf
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 194768a3b540511996e1d99e6450a7a9b24ebc74
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184294"
---
# <a name="commands-element"></a>Commands 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage のツールバーのコマンドのコレクションを表します。 コレクションは次のように最大 5 つのサブセクションを持つことができます: メニューのグループ、ボタン、combos、およびビットマップ。  
  
 各サブセクションの子要素、たとえば、\<メニュー >、GUID と数値識別子のペアである一意のコマンド ID によって識別されます。 GUID は、「コマンド セット」を識別し、論理的に関連するコマンドをグループ化するために使用します。 VSPackage では、その他の Vspackage で定義されているコマンド Id を持つ衝突を避けるために設定の独自のコマンドを定義します。  
  
## <a name="syntax"></a>構文  
  
```  
<Commands package="GuidMyPackage" >  
  <Menus>... </Menus>  
  <Groups>... </Groups>  
  <Buttons>... </Buttons>  
  <Combos>... </Combos>  
  <Bitmaps>... </Bitmaps>  
</Commands>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|パッケージ (package)|コマンドを提供する VSPackage を識別する GUID。<br /><br /> たとえば、パッケージ化"guidVsPackage1Pkg"を = です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[Menus 要素](../extensibility/menus-element.md)|VSPackage を実装するすべてのメニューを定義します。|  
|[Groups 要素](../extensibility/groups-element.md)|VSPackage ではコマンド グループを定義するエントリが含まれています。|  
|[Buttons 要素](../extensibility/buttons-element.md)|ボタン要素をグループ化します。|  
|[Bitmaps 要素](../extensibility/bitmaps-element.md)|ビットマップの要素をグループ化します。|  
|[Combos 要素](../extensibility/combos-element.md)|複合要素をグループ化します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[CommandTable 要素](../extensibility/commandtable-element.md)|IDE に VSPackage を提供するコマンドを表すすべての要素を定義します。 使用可能な要素は、メニュー項目、メニューのツールバー、およびコンボ ボックス。|  
  
## <a name="example"></a>例  
 次の例は、使用する方法を示します、[コマンド要素](../extensibility/commands-element.md)します。  
  
```  
<Commands package="guidMyPackage">  
    <Menus>  
      <Menu Condition="'%(DEBUG)' != 'true'"   
        guid="cmdSetGuidMyProductCommands" id="menuIDMainMenu"   
        priority="0x0000" type="Menu">  
        <Annotation>  
          <Documentation>this is an annotation</Documentation>  
          <AppInfo>  
            <CustomData>  
              <CustomSubElement>Some data</CustomSubElement>  
            </CustomData>  
          </AppInfo>  
        </Annotation>  
        <CommandFlag>AlwaysCreate</CommandFlag>  
        <Strings>  
          <ButtonText>MainMenu</ButtonText>  
        </Strings>  
      </Menu>  
  </Menus>  
<Commands>  
```  
  
## <a name="see-also"></a>関連項目  
 [Vspackage がユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
