---
title: Visual Studio コマンドの GUID および ID | Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) に含まれているコマンドの GUID と ID の値を見つける方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- commands
- id
- command placement
- visual studio command
- guid
ms.assetid: 2ea4bee2-0259-4675-8e65-2023b312b516
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8442e6430ead8f28d2afc7f51d14968b6999fcd9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898280"
---
# <a name="guids-and-ids-of-visual-studio-commands"></a>Visual Studio コマンドの GUID および ID
Visual Studio 統合開発環境 (IDE) に含まれるコマンドの GUID と ID の値は、Visual Studio SDK の一部としてインストールされる .vsct ファイルで定義されています。 詳細については、「[IDE 定義コマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)」を参照してください。

 *.vsct* ファイルで定義されている IDE オブジェクトを操作する方法の詳細については、「[メニューとコマンドを拡張する](../../extensibility/extending-menus-and-commands.md)」を参照してください。

## <a name="find-a-command-definition"></a>コマンド定義の検索
 Visual Studio では、1000 を超えるコマンドが定義されているため、ここですべてを一覧表示するのは現実的ではありません。 代わりに、次の手順に従ってコマンドの定義を検索します。

### <a name="to-locate-a-command-definition"></a>コマンド定義を検索するには

1. Visual Studio で、 *<Visual Studio SDK インストールパス\>\VisualStudioIntegration\Common\Inc\\* フォルダーにある、*SharedCmdDef.vsct*、*ShellCmdDef.vsct*、*VsDbgCmdUsed.vsct*、*Venusmenu.vsct* の各ファイルを開きます。

    ほとんどの Visual Studio コマンドは、*SharedCmdDef.vsct* と *ShellCmdDef.vsct* で定義されています。 *VsDbgCmdUsed.vsct* ではデバッガーに関連するコマンドを定義し、*Venusmenu.vsct* では Web 開発に固有のコマンドを定義します。

2. コマンドがメニュー項目の場合は、メニュー項目のテキストを正確に書き留めます。 コマンドがツールバーのボタンである場合は、一時停止したときに表示されるツールヒントのテキストを書き留めます。

3. **Ctrl**+**F** キーを押して **[検索]** ダイアログ ボックスを開きます。

4. **[検索する文字列]** ボックスに、手順 2 で書き留めたテキストを入力します。

5. **[検索対象]** ボックスに **[すべての開かれているドキュメント]** が表示されていることを確認します。

6. [ボタン要素](../../extensibility/button-element.md)の `<Strings>` セクションでテキストが選択されるまで、 **[次を検索]** ボタンをクリックします。

    コマンドが表示される `<Button>` 要素は、コマンド定義です。

   コマンド定義が見つかったら、コマンドと同じ `guid` および `id` 値を持つ [CommandPlacement 要素](../../extensibility/commandplacement-element.md)を作成することによって、コマンドのコピーを別のメニューまたはツールバーに配置できます。 詳細については、「[再利用可能なボタンのグループを作成する](../../extensibility/creating-reusable-groups-of-buttons.md)」を参照してください。

### <a name="special-cases"></a>特殊なケース
 次の場合、メニュー テキストまたはツールヒントのテキストが、コマンド定義の内容と正確に一致しない可能性があります。

- **[File]** メニューの **[Print]** コマンドなど、下線付きの文字を含むメニュー項目。*P* は下線付きで表示されます。

     メニュー項目名のアンパサンド (&) 文字の前にある文字が下線付きで表示されます。 ただし、 *.vsct* ファイルは XML で記述されます。この XML では、アンパサンド (&) 文字を使用して特殊文字を指定し、表示するアンパサンドを *&amp;amp;* として指定する必要があります。 したがって、 *.vsct* ファイルでは、 **[Print]** コマンドは *&amp;amp;Print* のように表示されます。

- **[\<Current Filename\> の保存]** などの動的なテキストを含むコマンドと、 **[最近使ったファイル]** 一覧にある項目などの動的に生成されたメニュー項目。

     動的テキストを検索するための信頼性の高い方法はありません。 代わりに、[Visual Studio メニューの GUID と ID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)、または [Visual Studio ツールバーの GUID と ID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md) を参照して、目的のコマンドをホストするグループを検索し、そのグループの ID を検索します。 コマンド定義にグループが [親要素](../../extensibility/parent-element.md)として含まれていない場合は、コマンドの親を設定する `<CommandPlacement>` 要素に対して、*SharedCmdPlace.vsct* と *ShellCmdPlace.vsct* (デバッガー コマンドの場合は *VsDbgCmdPlace.vsct*) を検索します。 *SharedCmdPlace.vsct*、*ShellCmdPlace.vsct*、および *VsDbgCmdPlace.vsct* は *\<Visual Studio SDK installation path\>\VisualStudioIntegration\Common\Inc\\* フォルダーにあります。

## <a name="see-also"></a>関連項目

- [Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)
