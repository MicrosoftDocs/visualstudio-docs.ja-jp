---
title: プロジェクト内のファイルを開くエディターの決定 | Microsoft Docs
description: プロジェクト内のファイルを開くエディターを決定するために Visual Studio で使用されるレジストリ キーおよび Visual Studio SDK のメソッドについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], determining which editor opens a file
- projects [Visual Studio SDK], determining which editor opens file
- project types, determining which editor opens a file
- persistence, determining which editor opens a file
ms.assetid: acbcf4d8-a53a-4727-9043-696a47369479
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fb6f142ea25748f6798fb60d7c03862c51819349
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090864"
---
# <a name="determine-which-editor-opens-a-file-in-a-project"></a>プロジェクト内のファイルを開くエディターを決定する
ユーザーがプロジェクト内のファイルを開くと、環境ではポーリング プロセスを実行し、最終的にそのファイルの適切なエディターまたはデザイナーを開きます。 環境で採用されている最初の手順は、標準のエディターとカスタム エディターの両方で同じです。 この環境では、ファイルを開くために使用するエディターをポーリングするときに、さまざまな基準を使用します。VSPackage では、このプロセス中に環境を調整する必要があります。

 たとえば、ユーザーが **[ファイル]** メニューから **[開く]** コマンドを選択し、*filename.rtf* (または *.rtf* 拡張子を持つその他のファイル) を選択すると、環境では各プロジェクトの <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> 実装が呼び出され、最終的にはソリューション内のすべてのプロジェクト インスタンスで順番にこれが行われます。 プロジェクトによって、優先度によってドキュメントの要求を識別するフラグのセットが返されます。 最も高い優先度を使用すると、環境では適切な <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> メソッドが呼び出されます。 ポーリング プロセスの詳細については、「[プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。

 その他のファイル プロジェクトでは、他のプロジェクトによって要求されないすべてのファイルを要求します。 これにより、ドキュメントを標準のエディターで開く前にカスタム エディターで開くことができます。 その他のファイル プロジェクトによってファイルが要求された場合、環境では <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> メソッドを呼び出して、標準のエディターでファイルを開きます。 環境では、登録済みエディターの内部リストで、 *.rtf* ファイルを処理するエディターを確認します。 このリストは、レジストリの次のキーにあります。

 **HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\\<version>\Editors\\\<editor factory guid>\Extensions**

 また、環境では、サブキー **DocObject** を持つすべてのオブジェクトの **HKEY_CLASSES_ROOT\CLSID** キーのクラス識別子も確認します。 ここでファイル拡張子が見つかった場合は、Microsoft Word などの埋め込みバージョンのアプリケーションが Visual Studio 内の現在の場所に作成されます。 これらのドキュメント オブジェクトは、<xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage> インターフェイスを実装する複合ファイルである必要があるか、またはオブジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> インターフェイスを実装する必要があります。

 レジストリに *.rtf* ファイルのエディター ファクトリがない場合は、環境で **HKEY_CLASSES_ROOT\\.rtf** キーを検索し、そこに指定されているエディターを開きます。 ファイル拡張子が **HKEY_CLASSES_ROOT** に見つからないとき、環境では Visual Studio のコア テキスト エディターを使用して、ファイルがテキスト ファイルである場合は開きます。

 コア テキスト エディターが失敗した場合 (ファイルがテキスト ファイルでないときに発生します)、環境ではファイルにバイナリ エディターを使用します。

 環境では、そのレジストリで *.rtf* 拡張子のエディターが見つかった場合、このエディター ファクトリを実装する VSPackage が読み込まれます。 環境で新しい VSPackage に対して <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> メソッドが呼び出されます。 VSPackage では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A> メソッドを使用して環境にエディター ファクトリを登録して、`SID_SVsRegistorEditor` の `QueryService` を呼び出します。

 次に環境では、 *.rtf* ファイル用に新しく登録されたエディター ファクトリを見つけるために、登録されているエディターの内部リストが再確認されます。 環境では、作成するファイル名とビューの種類を渡して、<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> メソッドの実装を呼び出します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>
- <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>
