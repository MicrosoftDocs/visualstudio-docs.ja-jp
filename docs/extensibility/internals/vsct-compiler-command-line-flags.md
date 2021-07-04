---
title: VSCT コンパイラのコマンドライン フラグ | Microsoft Docs
description: Visual Studio コマンド テーブル コンパイラは、.vsct ファイルのコンパイルを確実に成功させるためのコマンドライン オプションを提供します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT files, compiling
- command-table file compilation (VSCT files)
ms.assetid: 9dc6c33f-e6cf-4cf2-9b05-e8f7bfac1cfb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ce83df56e1bcfad50fe71da31291b5c43b26c47a
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898895"
---
# <a name="vsct-compiler-command-line-flags"></a>VSCT コンパイラのコマンドライン フラグ
Visual Studio コマンド テーブル (VSCT) コンパイラは、.vsct ファイルのコンパイルを確実に成功させるためのコマンドライン スイッチを提供します。

## <a name="command-line-parameters"></a>コマンドライン パラメーター
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の **[コマンド]** ウィンドウから基本的な VSCT ヘルプを表示するには、*Visual Studio SDK のインストール パス*\VisualStudioIntegration\Tools\Bin\ フォルダーに移動して、次のように入力します。

```
vsct /?
```

 次が返されます。

```
Microsoft (R) Visual Studio (R) Command Table Compiler Version 3.00.2000

Syntax: vsct <infile> [<outfile>] [-S[symbols file]] [-D<preprocessor-define>]*
[-I<include-path>]* [-L<language>] [-E[C|H|N]:<name>]

  -D    Specify any additional preprocessor defines
  -I    Indicate what additional include paths to send to the preprocessor
  -L    Specify the language to use when selecting strings
  -E    Emit C# objects in the specified namespace for command items,
        followed by [L|F|H|N]:<value>
        F = Name of the file to emit (used if -EL is provided)
        L = Name of a language providing a CodeDOM provider
        N = namespace (required if -EL is provided)
        H = C++ header
  -c    Clean build skipping dependency checks
  -v    Verbose output
```

> [!NOTE]
> コマンドライン パラメーターを示すための表記としては、- (ダッシュ) と / (スラッシュ) のどちらの文字も使用できます。

 指定できるフラグとその意味は次のとおりです。

|Switch|説明|
|------------|-----------------|
|-d|追加の定義済みシンボルを指定します。|
|-I|ファイル参照を解決するときに使用する追加のインクルード パスを示します。|
|-l|<xref:System.Globalization.CultureInfo> カルチャ名 (例: "en-US") を指定します。|
|-E|コマンド項目に対して指定された名前空間に C# オブジェクトを出力し、[C&#124;H&#124;N]:*filename* がその後に続きます。C は C#、H は C++ ヘッダー、N は名前空間を表します。 C# の場合、名前空間が必要です。|
|-v|詳細出力。|

 -L スイッチは、指定された <xref:System.Globalization.CultureInfo> カルチャ名に対応するバイナリ .cto ファイルを生成するために、文字列のグループを選択するようコンパイラに指示します。 指定されたカルチャ名は、.vsct ファイル内の 1 つ以上の [Strings 要素](../../extensibility/strings-element.md)の Language 属性と一致する必要があります。 Strings 要素に Language 属性がない場合、上位の [CommandTable 要素](../../extensibility/commandtable-element.md)から継承されます。

 .vsct ファイルには複数の Strings 要素が存在する場合があり、それぞれの Language 属性が異なっている場合があります。 グローバリゼーションを実現するには、VSCT コンパイラを複数回実行し、カルチャ名ごとに-L スイッチを変更します。

 -L スイッチで指定されたカルチャ名がどの Strings 要素の Language 属性にも一致しない場合、コンパイラは地域ではなく言語との一致を試みます。 たとえば、"en-US" が見つからない場合、コンパイラは代わりに "en" を試行します。 それにも失敗した場合、オペレーティング システムの現在のカルチャを試行します。 それにも失敗した場合、見つかった最初の Strings 要素をコンパイルします。

 -E スイッチを使用すると、コマンド テーブルによって使用されるシンボルを含む C スタイルのヘッダー ファイルを出力したり、コマンド シンボル用のオブジェクトを含む C# ファイルを出力したりできます。

 -D および -I スイッチには、同じ名前を持つ Cl.exe C プリプロセッサ フラグの構文があります。 X=Y 形式の -D 定義は、`Condition` 属性における XML ベースの \<Defined> テストの拡張に使用されます。 -I インクルード パスは、\<Include>、\<Extern>、\<Bitmap> の各ファイル参照を解決するために使用されます。 詳細については、「[VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)」を参照してください。

 VSCT コンパイラは、以前にビルドされたバイナリ ファイルを逆コンパイルすることもできます。 これを行うには、\<infile> にバイナリ ファイルを指定します。   バイナリ ファイルが VSCT コンパイラによって生成された場合、そのシンボルは既にファイルに埋め込まれています。また、出力の \<Symbols> セクションにシンボリック名を含む出力が生成されます。 バイナリが CTC コンパイラによって生成された場合、出力には実際の GUID と ID が含まれます。 現在のバージョンの Ctc.exe によって生成された *.ctsym ファイルがバイナリ入力ファイルと同じフォルダーにある場合、シンボルはそのファイルから読み込まれて出力に使用されます。

## <a name="see-also"></a>関連項目
- [Visual Studio Command Table (.Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
