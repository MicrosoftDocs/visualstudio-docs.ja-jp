---
title: 実行中のドキュメント テーブル | Microsoft Docs
description: メモリー内の開いているすべてのドキュメントを含め、実行中のドキュメント テーブルが Visual Studio IDE でどのように保持されるかを説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- read locks
- running document table (RDT), IVsDocumentLockHolder interface
- running document table (RDT)
- running document table (RDT), edit locks
- document data objects, running document table
ms.assetid: bbec74f3-dd8e-48ad-99c1-2df503c15f5a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d260534d58853afc6b84ba484eb3a806250e2aa6
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900409"
---
# <a name="running-document-table"></a>ドキュメント テーブルの実行
IDE では、現在開いているすべてのドキュメントの一覧が、実行中のドキュメント テーブル (RDT) と呼ばれる内部構造で保持されます。 この一覧には、これらのドキュメントが現在編集中かどうかに関係なく、メモリ内の開いているすべてのドキュメントが含まれます。 ドキュメントは、プロジェクトまたはメイン プロジェクト ファイル (.vcxproj ファイルなど) 内のファイルを含む、永続化された任意の項目です。

## <a name="elements-of-the-running-document-table"></a>実行中のドキュメント テーブルの要素
 実行中のドキュメント テーブルには、次のエントリが含まれています。

|要素|説明|
|-------------|-----------------|
|ドキュメント モニカー|ドキュメント データ オブジェクトを一意に識別する文字列。 これは、ファイルを管理するプロジェクト システムの絶対ファイル パスです (たとえば、C:\MyProject\MyFile)。 この文字列は、データベース内のストアド プロシージャなど、ファイル システム以外のストアに保存されたプロジェクトにも使用されます。 この場合、プロジェクト システムでは、ドキュメントを格納する方法を決定するために認識して解析できる一意の文字列を作成できます。|
|階層の所有者|ドキュメントを所有する階層オブジェクト。<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> インターフェイスによって表されます。|
|項目 ID|階層内の特定の項目の項目識別子。 この値は、このドキュメントを所有する階層内のすべてのドキュメント間で一意ですが、この値は異なる階層間で一意であるとは限りません。|
|ドキュメント データ オブジェクト|少なくとも、これは `IUnknown`<br /><br /> オブジェクト。 IDE では、カスタム エディターのドキュメント データ オブジェクトの `IUnknown` インターフェイスを超える特定のインターフェイスは必要ありません。 ただし、標準のエディターでは、プロジェクトからのファイル永続化呼び出しを処理するために、エディターの <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> インターフェイスの実装が必要です。 詳細については、「[標準ドキュメントの保存](../../extensibility/internals/saving-a-standard-document.md)」を参照してください。|
|フラグ|ドキュメントを保存するかどうかを制御するフラグ (読み取りまたは編集ロックを適用するかどうかなど) は、RDT にエントリを追加するときに指定できます。 詳細については、<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 列挙型のページをご覧ください。|
|編集ロック数|編集ロックの数。 編集ロックは、一部のエディターでドキュメントが編集用に開かれていることを示します。 編集ロックの数が 0 に遷移すると、ドキュメントが変更されている場合は、保存するように求められます。 たとえば、 **[新しいウィンドウ]** コマンドを使用してエディターでドキュメントを開くたびに、RDT にそのドキュメントの編集ロックが追加されます。 編集ロックを設定するには、ドキュメントに階層または項目 ID が必要です。|
|読み取りロック数|読み取りロックの数。 読み取りロックは、ドキュメントがウィザードなどの何らかのメカニズムによって読み取られていることを示します。 読み取りロックでは、ドキュメントを編集できないことを示しながら、RDT でドキュメントを有効な状態で保持します。 ドキュメントに階層または項目 ID がない場合でも、読み取りロックを設定できます。 この機能を使用すると、メモリ内のドキュメントを開いて、ドキュメントが階層によって所有されていなくても RDT で入力できます。 この機能はほとんど使用されません。|
|ロック ホルダー|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> インターフェイスのインスタンス。 ロック ホルダーは、エディター以外でドキュメントを開いたり編集したりするウィザードなどの機能によって実装されます。 ロック ホルダーを使用すると、編集ロックをドキュメントに追加して、まだ編集中のドキュメントが閉じられるのを防ぐことができます。 通常、編集ロックは、ドキュメント ウィンドウ (つまり、エディター) によってのみ追加されます。|

 RDT 内の各エントリには、一意の階層または項目 ID が関連付けられています。これは、通常、プロジェクト内の 1 つのノードに対応しています。 編集に使用できるすべてのドキュメントは、通常、階層によって所有されます。 RDT で作成されたエントリでは、どのプロジェクトが (より正確にはどの階層が)、編集中のドキュメント データ オブジェクトを現在所有しているかを制御します。 IDE では、RDT の情報を使用して、一度に複数のプロジェクトによってドキュメントが開かれないようにすることができます。

 階層では、データの永続性も制御され、RDT の情報を使用して **[保存]** および **[名前を付けて保存]** ダイアログ ボックスが更新されます。 ユーザーがドキュメントを変更した後、 **[ファイル]** メニューから **[終了]** コマンドを選択すると、IDE で **[変更の保存]** ダイアログ ボックスが表示され、現在変更されているすべてのプロジェクトとプロジェクト項目が示されます。 これにより、ユーザーは保存するドキュメントを選択できます。 保存するドキュメントの一覧 (変更されたドキュメント) は、RDT から生成されます。 アプリケーションの終了時に **[変更の保存]** ダイアログ ボックスに表示されるはずの項目には、RDT のレコードが含まれている必要があります。 RDT では、どのドキュメントを保存するかと、各ドキュメントの Flags エントリに指定された値を使用した保存操作についてユーザーに確認を求めるかどうかが調整されます。 RDT フラグの詳細については、<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 列挙型を参照してください。

## <a name="edit-locks-and-read-locks"></a>編集ロックと読み取りロック
 編集ロックと読み取りロックは RDT 内にあります。 ドキュメント ウィンドウでは、編集ロックを増減します。 このため、ユーザーが新しいドキュメント ウィンドウを開くと、編集ロック数は 1 ずつ増えます。 編集ロックの数が 0 になると、階層では、関連付けられているドキュメントのデータを保持または保存するように通知されます。 階層では、ファイルとして、またはリポジトリ内の項目として保持するなど、任意の方法でデータを保持することができます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> インターフェイスで <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.LockDocument%2A> メソッドを使用して、編集ロックと読み取りロックを追加したり、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> メソッドを使用してこれらのロックを解除したりできます。

 通常、エディターのドキュメント ウィンドウがインスタンス化されると、ウィンドウ フレームによって、RDT 内のドキュメントの編集ロックが自動的に追加されます。 ただし、標準のドキュメント ウィンドウを使用しない (つまり、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> インターフェイスを実装しない) ドキュメントのカスタム ビューを作成する場合は、独自の編集ロックを設定する必要があります。 たとえば、ウィザードでは、エディターで開かずにドキュメントが編集されます。 ウィザードと類似のエンティティによってドキュメント ロックが開かれるようにするには、これらのエンティティで <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> インターフェイスを実装する必要があります。 ドキュメントのロック ホルダーを登録するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> メソッドを呼び出し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> 実装を渡します。 そうすると、ドキュメントのロック ホルダーが RDT に追加されます。 ドキュメントのロック ホルダーを実装するもう 1 つのシナリオは、特殊なツール ウィンドウでドキュメントを開く場合です。 この場合は、ツール ウィンドウでドキュメントを閉じることはできません。 ただし、RDT でドキュメントのロック ホルダーとして登録することにより、IDE では <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder.CloseDocumentHolder%2A> メソッドの実装を呼び出して、ドキュメントを閉じるように求めることができます。

## <a name="other-uses-of-the-running-document-table"></a>実行中のドキュメント テーブルの他の用途
 IDE 内の他のエンティティでは、RDT を使用してドキュメントに関する情報を取得します。 たとえば、ソース管理マネージャーでは RDT を使用して、ファイルの最新バージョンを取得した後に、エディターでドキュメントを再読み込みするようにシステムに指示します。 これを行うには、ソース管理マネージャーで RDT 内のファイルを検索して、いずれかが開いているかどうかを調べます。 そうである場合、ソース管理マネージャーではまず、階層によって <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> メソッドが実装されていることを確認します。 プロジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> メソッドを実装していない場合、ソース管理マネージャーによって、ドキュメント データ オブジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> メソッドが実装されているかどうかが直接確認されます。

 また、ユーザーがドキュメントを要求した場合、IDE では RDT を使用して、開いているドキュメントを再浮上させます (前面に移動します)。 詳細については、「[ファイルを開くコマンドを使用したファイルの表示](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)」を参照してください。 ファイルが RDT で開いているかどうかを判別するには、次のいずれかを行います。

- ドキュメント モニカー (つまり、完全なドキュメント パス) に対してクエリを実行して、項目が開いているかどうかを確認します。

- 階層または項目 ID を使用して、プロジェクト システムに完全なドキュメント パスを要求してから、RDT で項目を検索します。

## <a name="see-also"></a>関連項目
- [RDT_ReadLock の使用法](../../extensibility/internals/rdt-readlock-usage.md)
- [ドキュメント テーブルの保存と実行](../../extensibility/internals/persistence-and-the-running-document-table.md)
