---
title: ドキュメントの読み込みの遅延 | Microsoft Docs
description: Visual Studio でのドキュメントの読み込みの遅延についてと、読み込まれる前にドキュメント内の要素に対してクエリを実行しないように拡張機能のコードを書く方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: fb07b8e2-a4e3-4cb0-b04f-8eb11c491f35
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 959af31f1986a4ff670adc5d74573cfb2bb850ce
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090984"
---
# <a name="delayed-document-loading"></a>ドキュメントの読み込みの遅延

ユーザーが Visual Studio ソリューションを再び開くと、関連付けられているドキュメントのほとんどはすぐに読み込まれません。 ドキュメント ウィンドウ フレームは、保留中の初期化状態で作成され、プレースホルダー ドキュメント (スタブ フレームと呼ばれます) が実行中のドキュメント テーブル (RDT) に配置されます。

拡張機能を使用すると、読み込まれる前にドキュメント内の要素に対してクエリを実行することで、プロジェクト ドキュメントが不必要に読み込まれる可能性があります。これで、Visual Studio のメモリ占有領域全体が増加する可能性があります。

## <a name="document-loading"></a>ドキュメントの読み込み

スタブ フレームとドキュメントは、ユーザーがたとえばウィンドウ フレームのタブを選択してドキュメントにアクセスしたときに、完全に初期化されます。 ドキュメントは、ドキュメント データを取得するために RDT に直接アクセスするか、次のいずれかの呼び出しを行って間接的に RDT にアクセスすることで、ドキュメントのデータを要求する拡張機能によって初期化することもできます。

- ウィンドウ フレームの <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> メソッド。

- 次のいずれかのプロパティのウィンドウ フレーム <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> メソッド。

  - [__VSFPROPID.VSFPROPID_DocView](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocView>)

  - [__VSFPROPID.VSFPROPID_ViewHelper](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ViewHelper>)

  - [__VSFPROPID.VSFPROPID_DocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocData>)

  - [__VSFPROPID.VSFPROPID_AltDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_AltDocData>)

  - [__VSFPROPID.VSFPROPID_RDTDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_RDTDocData>)

  - [__VSFPROPID.VSFPROPID_SPProjContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_SPProjContext>)

- 拡張機能でマネージド コードを使用するときは、ドキュメントが保留中の初期化状態でないことがわかっているか、ドキュメントを完全に初期化する必要がある場合を除き、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> を呼び出さないでください。 その理由は、メソッドによって常にドキュメント データ オブジェクトが返され、必要に応じて作成されるためです。 代わりに、`IVsRunningDocumentTable4` インターフェイスでいずれかのメソッドを呼び出す必要があります。

- 拡張機能で C++ が使用されている場合は、必要のないパラメーターで `null` を渡すことができます。

- 他のプロパティを要求する前に、関連するプロパティを要求する前に、次のいずれかのメソッドを呼び出すことによって、不要なドキュメントの読み込みを回避できます。

  - [__VSFPROPID6.VSFPROPID_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID6.VSFPROPID_PendingInitialization>) を使用する <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>。

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>. このメソッドでは、ドキュメントがまだ初期化されていない場合に [_VSRDTFLAGS4.RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>) の値を含む <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> オブジェクトを返します。

ドキュメントが読み込まれたタイミングは、ドキュメントが完全に初期化されたときに発生する RDT イベントをサブスクライブすることによって確認できます。 次の 2 つの可能性があります。

- イベント シンクで <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2> を実装している場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2.OnAfterAttributeChangeEx%2A> をサブスクライブできます。

- それ以外の場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterAttributeChange%2A> をサブスクライブできます。

次の例は、架空のドキュメント アクセス シナリオです。Visual Studio 拡張機能で、開いているドキュメントに関する情報 (たとえば、編集ロック数やドキュメント データに関する情報) を表示したいとします。 <xref:Microsoft.VisualStudio.Shell.Interop.IEnumRunningDocuments> を使用して RDT 内のドキュメントを列挙し、次に編集ロック数とドキュメント データを取得するために各ドキュメントで <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> を呼び出します。 ドキュメントが保留中の初期化状態である場合、ドキュメント データを要求すると、不必要に初期化されます。

ドキュメントにアクセスするためのより効率的な方法は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentEditLockCount%2A> を使用して編集ロック数を取得し、次に <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A> を使用してドキュメントが初期化されているかどうかを判断する方法です。 フラグに [_VSRDTFLAGS4.RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>) が含まれていない場合は、ドキュメントは既に初期化されており、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentData%2A> を使用してドキュメント データを要求しても、不必要に初期化は行われません。 フラグに [_VSRDTFLAGS4.RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>) が含まれている場合は、ドキュメントが初期化されるまで、拡張機能ではドキュメント データの要求を避ける必要があります。 この初期化は、`OnAfterAttributeChange(Ex)` イベント ハンドラーで検出できます。

## <a name="test-extensions-to-see-if-they-force-initialization"></a>拡張機能をテストして、初期化を強制的に実行するかどうかを確認する

ドキュメントが初期化されているかどうかを示す明白な手掛かりはありません。そのため、拡張機能で強制的に初期化されているかどうかを確認するのが困難な場合があります。 検証が簡単になるレジストリ キーを設定できます。これは、完全に初期化されていないすべてのドキュメントのタイトルのタイトルにテキスト *[Stub]* が表示されるようになるためです。

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0\BackgroundSolutionLoad** で、**StubTabTitleFormatString** を *{0} [Stub]* に設定します。
