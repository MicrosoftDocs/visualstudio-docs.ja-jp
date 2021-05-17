---
title: XML コマンド テーブル (.vsct) ファイルの設計 | Microsoft Docs
description: コマンド項目のレイアウトと外観 (ボタン、コンボ ボックス、メニュー、ツールバーなど) を記述する XML コマンド テーブル (.vsct) ファイルを設計する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, designing
ms.assetid: bb87a322-bac4-4258-92bc-9a876f05d653
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3d6409b5e624cd8596e669f191b2644aaf27a88c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090929"
---
# <a name="design-xml-command-table-vsct-files"></a>XML コマンド テーブル (.vsct) ファイルの設計
XML コマンド テーブル ( *.vsct*) ファイルでは、VSPackage のコマンド項目のレイアウトと外観が記述されています。 コマンド項目には、ボタン、コンボ ボックス、メニュー、ツールバー、およびコマンド項目のグループが含まれます。 この記事では、XML コマンド テーブル ファイル、コマンド項目とメニューに対する影響、およびそれらの作成方法について説明します。

## <a name="commands-menus-groups-and-the-vsct-file"></a>コマンド、メニュー、グループ、および. vsct ファイル
 *.vsct* ファイルは、コマンド、メニュー、およびコマンド グループを中心に構成されています。 *.vsct* ファイル内の XML タグは、これらの各項目を、コマンド ボタン、コマンドの配置、ビットマップなどの関連する他の項目と共に表します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] パッケージ テンプレートを実行して新しい VSPackage を作成すると、選択内容に応じて、テンプレートによってメニュー コマンド、ツール ウィンドウ、またはカスタム エディターに必要な要素を含む *.vsct* ファイルが生成されます。 その後、この *.vsct* ファイルを、特定の VSPackage の要件を満たすように変更することができます。 *.vsct* ファイルを変更する方法の例については、[メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)に関するページを参照してください。

 新しい空の *.vsct* ファイルを作成するには、[ *.vsct* ファイルを作成する方法](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)に関するページを参照してください。 作成したら、コマンド項目のレイアウトを記述するために、XML 要素、属性、および値をファイルに追加します。 詳細な XML スキーマについては、[VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)に関するページを参照してください。

## <a name="differences-between-ctc-and-vsct-files"></a>.ctc ファイルと .vsct ファイルの相違点
 *.vsct* ファイルの XML タグの背後にある意味は、現在は非推奨の *.ctc* ファイル形式のタグと同じですが、実装は少し異なります。

- 新しい **\<extern>** タグは、コンパイルする他の *.h* ファイル ([!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ツールバー用のファイルなど) を参照する場所です。

- *.vsct* ファイルでは **/include** ステートメントがサポートされていますが、 *.ctc* ファイルと同様に、新しい **\<import>** 要素も備えています。 違いは、 **/include** では "*すべて*" の情報が取り込まれるのに対し、 **\<import>** では名前だけが取り込まれることです。

- *.ctc* ファイルにはプリプロセッサ ディレクティブを定義するヘッダー ファイルが必要ですが、 *.vsct* ファイルには必要ありません。 代わりに、 *.vsct* ファイルの末尾にある、 **\<Symbol>** 要素に配置されているシンボル テーブルにディレクティブを配置します。

- *.vsct* ファイルには **\<Annotation>** タグがあり、これにより、メモや画像などの好きな情報を埋め込むことができます。

- 値は、項目に属性として格納されます。

- コマンド フラグは、個別に保存することも、スタックすることもできます。  ただし、IntelliSense は、スタックされたコマンド フラグでは機能しません。 コマンド フラグの詳細については、[CommandFlag 要素](../../extensibility/command-flag-element.md)に関するページを参照してください。

- 分割ドロップダウン、コンボなど、複数の種類を指定できます。

- GUID は検証されません。

- 各 UI 要素には、それと共に表示されるテキストを表す文字列があります。

- 親は省略可能です。 省略した場合、"*不明なグループ*" という値が使用されます。

- *Icon* 引数は省略可能です。

- Bitmap セクション: このセクションは *.ctc* ファイルと同じですが、コンパイル時に *vsct.exe* コンパイラによってプルされるファイル名を Href で指定できるようになった点が異なります。

- ResID: 古いビットマップ リソース ID を使用でき、 *.ctc* ファイルと同じように機能します。

- HRef: ビットマップ リソースのファイル名を指定できる新しいメソッド。 すべてが使用されていることを前提としているため、Used セクションは省略することができます。 コンパイラは、最初にファイルの、次に任意のネット共有のローカル リソースと、 **/I** スイッチによって定義されているすべてのリソースを検索します。

- キーバインド: エミュレーターを指定する必要はなくなりました。 いずれかを指定すると、コンパイラは、エディターとエミュレーターが同じであると見なします。

- Keychord: Keychord は削除されています。 新しい形式は、"*Key1,Mod1,Key2,Mod2*" です。  文字、16 進数、または VK 定数のいずれかを指定できます。

新しいコンパイラである *vsct.exe* は、 *.ctc* と *.vsct* の両方のファイルをコンパイルします。 ただし、古い *ctc.exe* コンパイラは、 *.vsct* ファイルを認識したりコンパイルしたりしません。

*vsct.exe* コンパイラを使用して、既存の *.cto* ファイルを *.vsct* ファイルに変換することができます。 詳細については、[既存の .cto ファイルから .vsct ファイルを作成する方法](../../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file)に関するページを参照してください。

## <a name="the-vsct-file-elements"></a>.vsct ファイルの要素
 コマンド テーブルには、次の階層と要素があります。

- [CommandTable 要素](../../extensibility/commandtable-element.md): VSPackage に関連付けられているすべてのコマンド、メニュー グループ、およびメニューを表します。

- [Extern 要素](../../extensibility/extern-element.md): *.vsct* ファイルとマージするすべての外部 .h ファイルを参照します。

- [Include 要素](../../extensibility/include-element.md): コンパイルする追加のヘッダー (.h) ファイルを、使用する *.vsct* ファイルと共に参照します。 *.vsct* ファイルには、IDE または別の VSPackage が提供するコマンド、メニュー グループ、およびメニューを定義する定数が含まれている *.h* ファイルを含めることができます。

- [Commands 要素](../../extensibility/commands-element.md): 実行可能な個々のコマンドのすべてを表します。 各コマンドには、次の 4 つの子要素があります。

- [Menus 要素](../../extensibility/menus-element.md): VSPackage のすべてのメニューとツールバーを表します。 メニューは、コマンドのグループのコンテナーです。

- [Groups 要素](../../extensibility/groups-element.md): VSPackage 内のすべてのグループを表します。 グループは、個々のコマンドのコレクションです。

- [Buttons 要素](../../extensibility/buttons-element.md): VSPackage 内のすべてのコマンド ボタンとメニュー項目を表します。 ボタンは、コマンドに関連付けることができる視覚的なコントロールです。

- [Bitmaps 要素](../../extensibility/bitmaps-element.md): VSPackage 内のすべてのボタンのすべてのビットマップを表します。 ビットマップは、コンテキストに応じてコマンド ボタンの横または上に表示される画像です。

- [CommandPlacements 要素](../../extensibility/commandplacements-element.md): VSPackage のメニューに個々のコマンドを配置する必要がある追加の場所を示します。

- [VisibilityConstraints 要素](../../extensibility/visibilityconstraints-element.md): コマンドを常に表示するか、特定のコンテキスト (特定のダイアログ ボックスやウィンドウが表示されるときなど) でのみ表示するかを指定します。 この要素の値を持つメニューとコマンドは、指定されたコンテキストがアクティブな場合にのみ表示されます。 既定の動作では、コマンドは常に表示されます。

- [KeyBindings 要素](../../extensibility/keybindings-element.md): コマンドのキー バインドを指定します。 つまり、**Ctrl**+**S** など、コマンドを実行するために押す必要がある 1 つまたは複数のキーの組み合わせです。

- [UsedCommands 要素](../../extensibility/usedcommands-element.md): 指定されたコマンドは他のコードによって実装されているが、現在の VSPackage がアクティブな場合はコマンドの実装を提供することを、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 環境に通知します。

- [Symbols 要素](../../extensibility/symbols-element.md): パッケージ内のすべてのコマンドのシンボル名と GUID ID が含まれます。

## <a name="vsct-file-design-guidelines"></a>. vsct ファイルの設計のガイドライン
 *.vsct* ファイルを正常に設計するには、次のガイドラインに従ってください。

- コマンドはグループ内にのみ配置でき、グループはメニュー内にのみ配置でき、メニューはグループ内にのみ配置できます。 実際には、IDE にはメニューのみが表示され、グループとコマンドは表示されません。

- サブメニューをメニューに直接割り当てることはできませんが、次にメニューに割り当てられるグループに割り当てる必要があります。

- コマンド、サブメニュー、およびグループは、定義するディレクティブの親フィールドを使用して、1 つのペアレンティング グループまたはメニューに割り当てることができます。

- ディレクティブ内の親フィールドだけを使用したコマンド テーブルの編成には、かなりの制限があります。 オブジェクトを定義するディレクティブは、1 つの親引数のみを取ることができます。

- コマンド、グループ、またはサブメニューを再利用するには、新しいディレクティブを使用して、オブジェクトの新しいインスタンスを独自の `GUID:ID` ペアで作成する必要があります。

- `GUID:ID` の各ペアは、一意である必要があります。 たとえば、メニュー、ツールバー、またはコンテキスト メニューに配置されたコマンドの再利用は、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスによって処理されます。

- コマンドとサブメニューを複数のグループに割り当てることもでき、[Commands 要素](../../extensibility/commands-element.md)を使用してグループを複数のメニューに割り当てることができます。

## <a name="vsct-file-notes"></a>.vsct ファイルの注意事項
 *.vsct* ファイルをコンパイルしてネイティブのサテライト DLL に配置した後で変更を加える場合は、**devenv.exe/setup/nosetupvstemplates** を実行する必要があります。 これにより、実験用のレジストリに指定されている VSPackage リソースの再読み込みと、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] が記述されている内部データベースの再構築が、強制的に行われます。

 開発時には、複数の VSPackage プロジェクトが作成され、実験用のレジストリ ハイブに登録される可能性があります。これにより、IDE で混乱を招く可能性があります。 この問題を解決するには、実験用のハイブを既定の設定にリセットして、登録されているすべての Vspackage と、IDE に加えられたすべての変更を削除します。 実験用のハイブをリセットするには、Visual Studio SDK に付属の CreateExpInstance.exe ツールを使用します。 これは次の場所にあります。

 *%PROGRAMFILES(x86)%\Visual Studio\\\<version> SDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe*

 **CreateExpInstance/Reset** コマンドを使用して、ツールを実行します。 このツールは、通常は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] でインストールされていない登録済みのすべての VSPackage を、実験用のハイブから削除することに注意してください。

## <a name="see-also"></a>関連項目
- [メニューとコマンドを拡張する](../../extensibility/extending-menus-and-commands.md)
