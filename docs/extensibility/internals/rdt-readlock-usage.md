---
title: RDT_ReadLock の使用法 | Microsoft Docs
description: 実行中のドキュメント テーブル内のドキュメントをロックするためのロジックが用意されている _VSRDTFLAGS.RDT_ReadLock フラグについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- RDT_ReadLock
- visible
- RDT_EditLock
- invisible
ms.assetid: b935fc82-9d6b-4a8d-9b70-e9a5c5ad4a55
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6add02e763c9664c19fe21b1cfc37dd29b3010b9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060836"
---
# <a name="rdt_readlock-usage"></a>RDT_ReadLock の使用法

[_VSRDTFLAGS.RDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>) は、実行中のドキュメント テーブル (RDT) (Visual Studio IDE で現在開かれているすべてのドキュメントの一覧) 内のドキュメントをロックするためのロジックが用意されているフラグです。 このフラグを使用すると、ドキュメントがいつ開かれるか、またドキュメントがユーザー インターフェイスで可視になるか、不可視の状態でメモリに保持されるかを決定することができます。

通常、次のいずれかに該当する場合は、[_VSRDTFLAGS.RDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>) を使用します。

- ドキュメントを不可視の状態かつ読み取り専用で開きたいが、それを所有する <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> がまだ確立されていない。

- 不可視の状態で開かれたドキュメントをユーザーが UI で表示してから閉じる前に、保存するようにユーザーに求めるプロンプトを表示する必要がある。

## <a name="how-to-manage-visible-and-invisible-documents"></a>可視および不可視のドキュメントを管理する方法

ユーザーが UI でドキュメントを開いたら、ドキュメントの <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> の所有者を確立し、[_VSRDTFLAGS.RDT_EditLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_EditLock>) フラグを設定する必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> の所有者を確立できない場合、ユーザーが **[すべて保存]** をクリックするか、IDE を閉じても、ドキュメントは保存されません。 つまり、ドキュメントが不可視の状態で開かれ、それがメモリ内で変更され、シャットダウン時にドキュメントを保存するようにユーザーが求められた場合、または **[すべて保存]** が選択されて保存された場合、`RDT_ReadLock` は使用できません。 代わりに `RDT_EditLock` を使用して、[__VSREGDOCLOCKHOLDER.RDLH_WeakLockHolder](<xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER.RDLH_WeakLockHolder>) フラグが立ったときに <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> を登録する必要があります。

## <a name="rdt_editlock-and-document-modification"></a>RDT_EditLock とドキュメントの変更

前述のフラグは、不可視でドキュメントが開かれた場合、ユーザーによってそのドキュメントが開かれたときに `RDT_EditLock` が生成され、可視の **DocumentWindow** になることを示します。 これが発生すると、可視の **DocumentWindow** が閉じられたときに、ユーザーに **[保存]** プロンプトが表示されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> サービスを使用する `Microsoft.VisualStudio.Package.Automation.OAProject.CodeModel` の実装は、最初は `RDT_ReadLock` のみが取得された場合 (つまり、情報を解析するためにドキュメントが不可視の状態で開かれた場合) に機能します。 その後、ドキュメントを変更する必要がある場合に、ロックは弱い **RDT_EditLock** にアップグレードされます。 次に、ユーザーが可視の **DocumentWindow** でドキュメントを開くと、`CodeModel` の弱い `RDT_EditLock` は解放されます。

次に、ユーザーが **DocumentWindow** を閉じ、開かれているドキュメントを保存するように求められたときに **[いいえ]** を選択すると、`CodeModel` の実装により、ドキュメント内のすべての情報が破棄され、次にドキュメントについて追加の情報が必要になったときは、ディスクから不可視の状態でドキュメントが再度開かれます。 この動作の微妙な点は、不可視の開かれているドキュメントの **DocumentWindow** をユーザーが開き、変更して閉じ、ドキュメントの保存を求められたときに **[いいえ]** を選択するという例であることです。 この場合、ドキュメントに `RDT_ReadLock` があると、ユーザーがドキュメントを保存しないことを選択した場合でも、ドキュメントは実際には閉じられず、変更されたドキュメントはメモリ内で不可視の状態で開かれたままになります。

不可視の状態で開かれているドキュメントに弱い `RDT_EditLock` が使用されている場合、ユーザーが可視の状態でドキュメントを開いたときに、他のロックがかかっていなければ、そのロックは解除されます。 ユーザーが **DocumentWindow** を閉じ、ドキュメントを保存するように求められたときに **[いいえ]** を選択した場合、メモリからドキュメントを閉じる必要があります。 つまり、この発生を追跡するには、不可視のクライアントから RDT イベントをリッスンする必要があります。 次にドキュメントが必要になったときは、ドキュメントを再度開く必要があります。
