---
title: '[新しい項目の追加] ダイアログ ボックスに項目を追加する | Microsoft Docs'
description: Visual Studio の [新しい項目の追加] ダイアログ ボックスに項目を追加して、プロジェクトで使用するテンプレートとプロジェクトの要素を表示できるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, adding items
ms.assetid: 2f70863b-425b-4e65-86b4-d6a898e29dc7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 574cc5384018d14fdc05a834876002bbcbdbaaf7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079100"
---
# <a name="add-items-to-the-add-new-item-dialog-box"></a>[新しい項目の追加] ダイアログ ボックスに項目を追加する
**[新しい項目の追加]** ダイアログ ボックスに項目を追加するプロセスは、レジストリ キーから始めます。 次のレジストリ エントリに示すように、**AddItemTemplates** セクションには、 **[新しい項目の追加]** ダイアログ ボックスで使用できる項目が配置されているディレクトリのパスと名前が含まれています。

> [!NOTE]
> コード セグメントの直後のテーブルには、レジストリ エントリに関する追加情報が含まれています。

 このセクションは、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0Exp\Projects** の下にあります。

 最初の GUID は、この種類のプロジェクトの CLSID です。2 番目の GUID は、項目の追加テンプレートに登録されているプロジェクトの種類を示します。

 **\\{C061DB26-5833-11D2-96F5-000000000000}\\AddItemTemplates\\TemplatesDir\\{ACEF4EB2-57CF-11D2-96F4-000000000000}\\1**

 **@** = #6

 **TemplatesDir** = \\&lt;Visual Studio SDK installation path&gt;\\VSIntegration\\&lt;SomeFolder&gt;\\&lt;SomePackage&gt;\\&lt;SomeProject&gt;\\&lt;SomeProjectItems&gt;

 **SortPriority** = dword:00000064

| 名前 | Type | データ ( *.rgs* ファイルから) | 説明 |
|------------------|-----------| - | - |
| @ (既定値) | REG_SZ | #%IDS_ADDITEM_TEMPLATES_ENTRY% | **項目の追加** テンプレートのリソース ID。 |
| Val TemplatesDir | REG_SZ | %TEMPLATE_PATH%\\&lt;SomeProjectItems&gt; | **[新しい項目の追加]** ウィザードのダイアログに表示されるプロジェクト項目のパス。 |
| Val SortPriority | REG_DWORD | 100 ([!INCLUDE[vcprx64](../../extensibility/internals/includes/vcprx64_md.md)]) | **[新しい項目の追加]** ダイアログ ボックスに表示されるファイルのツリー ノード内の並べ替え順序を決定します。 |

> [!NOTE]
> Visual C# と Visual Basic のプロジェクトの種類の GUID は次のとおりです。
> - [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]: {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}
> - [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]: {F184B08F-C81C-45F6-A57F-5ABD9991F28F}

 **TemplatesDir**( *%TEMPLATE_PATH%\\&lt;SomeProjectItems&gt;* ) にリストされているディレクトリは、 **[新しい項目の追加]** ダイアログ ボックスのツリーの左側にあるノードです。 ツリー内のその他の要素は、そのルート ディレクトリ内のサブディレクトリに基づいています。 プロジェクトに追加できるファイルは、 **[新しい項目の追加]** ダイアログ ボックスの右ペインの項目です。

 通常、このフォルダーには、テンプレート HTML や *.cpp* ファイルなどのプロジェクトのテンプレート ファイルと、ウィザードを開始するための *.vsz* ファイルが含まれています。 項目の表示方法を制御するには、ディレクトリ名とアイコンをローカライズするための *.vsdir* ファイルを含めることもできます。 ローカライズされた文字列は、 **[新しい項目の追加]** ダイアログ ボックスのツリー内のこのノードを表すダイアログ ボックスに表示されるキャプションです。

 ただし、すべてのファイルを 1 つの *.vsdir* ファイルに含める必要はありません。 ディレクトリ内のすべての項目に対して 1 つの *.vsdir* ファイルを使用できます。 詳細については、「[ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)」と「[テンプレート ディレクトリの説明 (.vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)」を参照してください。

> [!NOTE]
> テンプレート ディレクトリ内の *.vsdir* ファイルはオプションです。 プロジェクト要素をディレクトリに配置して、 **[新しい項目の追加]** ダイアログ ボックスに表示するだけの場合は、**TemplatesDir** ステートメントで指定されているテンプレート ディレクトリにそのファイルを配置できます。 その後、そのプロジェクトの **[新しい項目の追加]** ダイアログ ボックスの右ペインに、そのファイルが表示されます。 ただし、ファイルまたはアイコンのローカライズされたキャプションを表示する場合は、テンプレート ディレクトリに少なくとも 1 つの *.vsdir* ファイルを含める必要があります。

## <a name="group-project-items"></a>プロジェクトの項目をグループ化する
 **[新しい項目の追加]** ダイアログ ボックスのツリーのフォルダーにテンプレート グループを含める場合は、ルート テンプレート ディレクトリの下にサブディレクトリがあり、その中に項目が含まれている必要があります。 **[新しい項目の追加]** ダイアログ ボックスがユーザーに表示されると、サブフォルダーも表示され、そこからプロジェクト要素を選択できます。

 コード セグメント内の並べ替えの優先順位によって、ツリー内のこのテンプレート ディレクトリが作成される場所が、ツリー ノードの他の要素に対する相対位置として決まります。 **[新しい項目の追加]** ダイアログ ボックスには、並べ替えの優先順位を含める必要があるだけです。これにより、項目がダイアログ ボックスの正しい場所に表示されるようになります。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>[新しい項目の追加]**ダイアログ ボックスに表示される内容をフィルター処理するための** インターフェイスを実装することもできます。 このインターフェイスを実装することで、たとえば、50 個のテンプレート ファイルとウィザード ファイルを含む 1 つのテンプレート ディレクトリをディスク上にセットアップできます。 この方法では、あるプロジェクトの種類に属する 20 個のファイル、別のプロジェクトの種類に属する他の 30 個のファイル、および一般的な種類のプロジェクトで使用できるすべてのファイルを持つさまざまなプロジェクトの種類を持つことができます。 このようにして、作成されるプロジェクト テンプレートに応じて、一連の異なるテンプレート ファイルを表示できます。

 たとえば、Visual Basic プロジェクトに Web プロジェクトとクライアント プロジェクトがある場合があります。 Web フォームはクライアント プロジェクトに追加するのに便利な項目ではなく、ウィンドウズ フォームは Web サーバー プロジェクトに追加するのに便利な項目ではありません。 そのため、両方の種類のプロジェクトのすべてのファイルを含む 1 つのテンプレート ディレクトリを作成できます。 次に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> を実装することで、プロジェクトでプロジェクトの種類またはプロジェクト設定に基づいて表示しない項目を非表示にすることができます。

## <a name="filter-project-items"></a>プロジェクトの項目をフィルター処理する
 `IVsFilterAddProjectItemDlg2` では、次の方法でツリー (左側のペイン) とプロジェクト ファイル (右側のペイン) の要素をフィルター処理できます。

- `IVsFilterAddProjectItemDlg` によって提供される、ローカライズされた名前別 ( *.vsdir* ファイルに含まれている、ダイアログ ボックスに表示されるキャプション)。

- `IVsFilterAddProjectItemDlg` によって提供される、ディスク上のファイルおよびフォルダーの実際の名前別 (ローカライズされていない — *.vsdir* ファイルがない)。

- `IVsFilterAddProjectItemDlg2` によって提供されるカテゴリ別。

  カテゴリでフィルター処理するには、 *.vsdir* ファイル内の項目にカテゴリ文字列 (Visual Basic の "*Web フォーム*" や "*クライアント項目*" など) を指定します。 次に、ダイアログ ボックスのコードで *.vsdir* ファイルからカテゴリの分類を取得して、それを入手します。 その後、その情報を `IVsFilterAddProjectItemDlg2` の実装に渡すと、 **[新しい項目の追加]** ダイアログ ボックスをカテゴリ別にフィルター処理できます。 Web ページの項目をフィルター処理したり、クライアントの Win32 アプリケーションのケースとしてフィルター処理したりすることもできます。 また、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] のタグ付き項目は、Microsoft Foundation Classes (MFC) または Active Template Library (ATL) の項目として識別できます。 これらの項目を識別すると、プロジェクト システムで独自の分類を定義して、カテゴリと分類に基づいてシステムをフィルター処理できるようにすることができます。

  このフィルター機能を実装する場合、非表示にする必要があるすべての項目のテーブルをマップする必要はありません。 単純に項目を種類に分類し、その分類を *.vsdir* ファイルに含めることができます。 その後、インターフェイスを実装することによって、特定の分類を持つすべての項目を非表示にすることができます。 このようにして、 **[新しい項目の追加]** ダイアログ ボックスの項目を、プロジェクト内の状態に基づいて動的にすることができます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [プロジェクトの拡張に通常使用されるオブジェクトの CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [テンプレート ディレクトリの説明 (.vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
- [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
