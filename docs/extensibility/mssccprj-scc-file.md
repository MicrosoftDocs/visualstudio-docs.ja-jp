---
title: MSSCCPRJ.SCC ファイル | Microsoft Docs
description: Visual Studio SDK で動作するソース管理プラグインによって使用されるクライアント側のローカル ファイルである MSSCCPRJ.SCC ファイルについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, MSSCCPRJ.SCC file
- MSSCCPRJ.SCC file
ms.assetid: 6f2e39d6-b79d-407e-976f-b62a3cedd378
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 945d1a4d1acde0ac3fef9918123f963cf27127f1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090552"
---
# <a name="mssccprjscc-file"></a>MSSCCPRJ.SCC ファイル
IDE を使用して Visual Studio ソリューションまたはプロジェクトをソース管理下に置くと、IDE では 2 つの重要な情報を受け取ります。 これらの情報は、ソース管理プラグインから文字列の形式で渡されます。 これらの文字列 "AuxPath" と "ProjName" は、IDE にとっては不透明ですが、バージョン管理内のソリューションまたはプロジェクトを見つけるためにプラグインによって使用されます。 IDE では通常、[SccGetProjPath](../extensibility/sccgetprojpath-function.md) を呼び出してこれらの文字列を初めて取得した後、それを将来の [SccOpenProject](../extensibility/sccopenproject-function.md) の呼び出しのためにソリューションまたはプロジェクト ファイルに保存します。 ソリューションおよびプロジェクト ファイルに埋め込まれている場合、文字列 "AuxPath" と "ProjName" は、バージョン管理内にあるソリューションおよびプロジェクト ファイルをユーザーがブランチ、フォーク、またはコピーしても自動的には更新されません。 ソリューションおよびプロジェクト ファイルがバージョン管理内のその正しい場所を確実に指すようにするには、ユーザーがそれらの文字列を手動で更新する必要があります。 これらの文字列は意図的に不透明になっているため、その更新方法が常に明確であるとは限らない可能性があります。

 ソース管理プラグインでは、文字列 "AuxPath" と "ProjName" を *MSSCCPRJ.SCC* ファイルという名前の特殊なファイルに格納することによってこの問題を回避できます。 これは、プラグインによって所有および管理される、クライアント側のローカル ファイルです。 このファイルは、ソース管理下に置かれることはなく、ソース管理されたファイルが含まれているディレクトリごとにプラグインによって生成されます。 どのファイルが Visual Studio ソリューションおよびプロジェクト ファイルであるかを特定するために、ソース管理プラグインでは、ファイル拡張子を標準の一覧またはユーザーが指定した一覧と比較できます。 IDE では、プラグインが *MSSCCPRJ.SCC* ファイルをサポートしていることを検出すると、文字列 "AuxPath" と "ProjName" をソリューションおよびプロジェクト ファイルに埋め込むことを停止し、代わりに *MSSCCPRJ.SCC* ファイルからこれらの文字列を読み取ります。

 *MSSCCPRJ.SCC* ファイルをサポートするソース管理プラグインは、次のガイドラインに従う必要があります。

- *MSSCCPRJ.SCC* ファイルは、ディレクトリあたり 1 つしか存在できません。

- *MSSCCPRJ.SCC* ファイルには、特定のディレクトリ内でソース管理下にある複数のファイルの "AuxPath" と "ProjName" を含めることができます。

- "AuxPath" 文字列の中に引用符を含めることはできません。 区切り記号として前後に引用符を付けることは許可されます (たとえば、二重引用符のペアを使用して空の文字列を示すことができます)。 IDE では、*MSSCCPRJ.SCC* ファイルから "AuxPath" の文字列を読み取ると、そこからすべての引用符を削除します。

- *MSSCCPRJ.SCC ファイル*  内の "ProjName" の文字列は、`SccGetProjPath` 関数から返される文字列に正確に一致している必要があります。 この関数によって返される文字列の前後に引用符が付いている場合は、*MSSCCPRJ.SCC* ファイル内の文字列の前後にも引用符が付いている必要があり、その逆も同じです。

- *MSSCCPRJ.SCC* ファイルは、ファイルがソース管理下に置かれるたびに作成または更新されます。

- *MSSCCPRJ.SCC* ファイルが削除された場合、プロバイダーでは、次回そのディレクトリに関するソース管理操作を実行するときに、そのファイルを再生成する必要があります。

- *MSSCCPRJ.SCC* ファイルは、定義された形式に厳密に従う必要があります。

## <a name="an-illustration-of-the-mssccprjscc-file-format"></a>MSSCCPRJ.SCC のファイル形式の図
 *MSSCCPRJ.SCC* のファイル形式のサンプルを次に示します (行番号はガイドとしてのみ示されており、ファイル本体には含めないでください)。

- [1 行目] `SCC = This is a Source Code Control file`

- [2 行目]

- [3 行目] `[TestApp.sln]`

- [4 行目] `SCC_Aux_Path = "\\server\vss\"`

- [5 行目] `SCC_Project_Name = "$/TestApp"`

- [6 行目]

- [7 行目] `[TestApp.csproj]`

- [8 行目] `SCC_Aux_Path = "\\server\vss\"`

- [9 行目] `SCC_Project_Name = "$/TestApp"`

 最初の行には、このファイルの目的が記述されます。この行は、この種類のすべてのファイルの署名として機能します。 この行は、すべての *MSSCCPRJ.SCC* ファイルで、このように正確に記述される必要があります。

 `SCC = This is a Source Code Control file`

 次のセクションは各ファイルの設定の詳細を示し、ファイル名が角かっこで囲まれています。 このセクションは、追跡されるファイルごとに繰り返されます。 この行は、ファイル名のサンプル (つまり、`[TestApp.csproj]`) です。 IDE では、次の 2 行を予期しています。 ただし、定義される値のスタイルは定義されていません。 これらの変数は `SCC_Aux_Path` と `SCC_Project_Name` です。

 `SCC_Aux_Path = "\\server\vss\"`

 `SCC_Project_Name = "$/TestApp"`

 このセクションには終了区切り記号がありません。 このファイルの名前のほか、このファイルに現れるリテラルはすべて、scc.h ヘッダー ファイルで定義されています。 詳細については、「[ソース管理プラグインを検索するためのキーとして使用される文字列](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [ソース管理プラグインを検索するためのキーとして使用される文字列](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)
