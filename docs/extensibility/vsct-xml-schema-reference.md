---
title: VSCT XML スキーマ リファレンス | Microsoft Docs
description: VSCT XML スキーマのリファレンス記事では、コマンド テーブル コンパイラのスキーマ要素について説明し、それぞれで使用できる子要素と属性を示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Visual Studio command table configuration files (VSCT), XML schema
- VSCT XML schema elements
ms.assetid: 49e7efae-e713-4762-a824-96fdaf92cdc9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7d82cda9c91642b094deea50eda02676f9bb73f3
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905229"
---
# <a name="vsct-xml-schema-reference"></a>VSCT XML スキーマ リファレンス
コマンド テーブル コンパイラのスキーマ要素と、それぞれで使用できる子要素と属性をまとめた表を提供します。

 XML ベースのコマンド テーブル構成 (.vsct) ファイルでは、VSPackage から統合開発環境 (IDE) に提供されるコマンド要素を定義します。 これら要素には、メニュー項目、メニュー、ツール バー、コンボ ボックスが含まれます。

> [!NOTE]
> VSCT コンパイラでは、.vsct ファイルに対してプリプロセッサを実行できます。 これは通常 C++ プリプロセッサであるため、C++ ファイルで使用されているのと同じ構文を持つインクルードとマクロを定義できます。 これの例は、**新しいプロジェクト** ウィザードで VSPackage プロジェクト用に作成される .vsct ファイルで提供されます。

## <a name="optional-elements"></a>オプションの要素
 VSCT のいくつかの要素は省略可能です。 `Parent` 引数が指定されていない場合は、Group_Undefined:0 が暗黙的に指定されます。 `Icon` 引数が指定されていない場合は、guidOfficeIcon:msotcidNoIcon が暗黙的に指定されます。 ショートカット キーが定義されている場合、通常使用されないエミュレーションは省略可能です。

 ビットマップ項目は、コンパイル時に `href` 引数にビットマップ ストリップの場所を指定することで、埋め込むことができます。 ビットマップ ストリップは、DLL のリソースから抽出されるのではなく、マージ中にコピーされます。 `href` 引数を指定した場合、`usedList` 引数は省略可能になり、ビットマップ ストリップのすべてのスロットが使用されていると見なされます。

 すべての GUID と ID の値は、シンボル名を使用して定義する必要があります。 これらの名前は、ヘッダー ファイルまたは VSCT の \<Symbols> セクションで定義できます。 シンボル名は、ローカルにするか、\<Include> 要素を使用してインクルードするか、または \<Extern> 要素で参照する必要があります。 シンボル名は、\<Extern> 要素で指定されるヘッダー ファイルからインポートされます (「#define シンボル   値」の単純なパターンに従っている場合)。 この値として、別のシンボルを使用することもできます (そのシンボルが既に定義されている場合)。 GUID 定義は、OLE 形式または C++ 形式のいずれかに従う必要があります。 ID 値には、次の行に示すように、10 進数または 0x で始まる 16 進数を指定できます。

- {6D484634-E53D-4a2c-ADCB-55145C9362C8}

- { 0x6d484634, 0xe53d, 0x4a2c, { 0xad, 0xcb, 0x55, 0x14, 0x5c, 0x93, 0x62, 0xc8 } }

  XML コメントを使用することもできますが、ラウンドトリップ グラフィカル ユーザー インターフェイス (GUI) ツールでは、それらが破棄される場合があります。 \<Annotation> 要素の内容は、形式に関係なく維持されることが保証されます。

## <a name="schema-hierarchy"></a>スキーマの階層
 .vsct ファイルの主な要素は次のとおりです。

- [CommandTable 要素](../extensibility/commandtable-element.md)

- [Extern 要素](../extensibility/extern-element.md)

- [Include 要素](../extensibility/include-element.md)

- [Define 要素](../extensibility/define-element.md)

- [Commands 要素](../extensibility/commands-element.md)

- [CommandPlacements 要素](../extensibility/commandplacements-element.md)

- [VisibilityConstraints 要素](../extensibility/visibilityconstraints-element.md)

- [KeyBindings 要素](../extensibility/keybindings-element.md)

- [UsedCommands 要素](../extensibility/usedcommands-element.md)

- [親要素](../extensibility/parent-element.md)

- [Icon 要素](../extensibility/icon-element.md)

- [Strings 要素](../extensibility/strings-element.md)

- [コマンド フラグ要素](../extensibility/command-flag-element.md)

- [Symbols 要素](../extensibility/symbols-element.md)

- [Conditional 属性](../extensibility/vsct-xml-schema-conditional-attributes.md)

## <a name="see-also"></a>関連項目
- [VSPackage でユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [VSPackage のコマンド ルーティング](../extensibility/internals/command-routing-in-vspackages.md)
