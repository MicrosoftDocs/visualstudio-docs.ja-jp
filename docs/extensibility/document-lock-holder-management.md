---
title: ドキュメント ロック ホルダーの管理 |Microsoft Docs
description: ドキュメント ウィンドウで開いているドキュメントをユーザーに表示せずに、実行中のドキュメント テーブル内のドキュメントに対して編集ロックを設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document locking
ms.assetid: fa1ce513-eb7d-42bc-b6e8-cb2433d051d5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 88e66ed3b0a5434f4d875bf941e3eeffb8adc092
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091189"
---
# <a name="document-lock-holder-management"></a>ドキュメント ロック ホルダーの管理

実行中のドキュメント テーブル (RDT) では、開いているドキュメントの数と、設定されているすべての編集ロックが保持されます。 ドキュメント ウィンドウで開いているドキュメントをユーザーに表示せずに、ドキュメントがプログラムによってバックグラウンドで編集されているときに、RDT でドキュメントに編集ロックを設定できます。 この機能は、グラフィカル ユーザー インターフェイスを使用して複数のファイルを変更するデザイナーによってよく使用されます。

## <a name="document-lock-holder-scenarios"></a>ドキュメント ロック ホルダーのシナリオ

### <a name="file-a-has-a-dependence-on-file-b"></a>ファイル "a" はファイル "b" に依存している

ファイルの種類が "a" の標準のエディター "A" を実装し、種類が "a" の各ファイルに種類が "b" のファイルへの参照 (またはその依存) がある状況について考えてみます。 種類が "b" のファイルには、標準のエディター "B" が存在します。 エディター "A" でファイル "a" を開くと、対応するファイル "b" への参照が取得されます。 ファイル "b" は表示されませんが、エディター "A" では変更できます。 エディター "A" では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> メソッドからファイル "b" のドキュメント データへの参照を取得し、ファイル "b" の編集ロックも保持します。 エディター "A" でファイル "b" の変更が完了すると、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> メソッドを呼び出すことによって、ファイル "b" の編集ロック数を減らすことができます。 パラメーター `dwRDTLockType` を [_VSRDTFLAGS.RDT_NoLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_NoLock>) に設定して <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> メソッドを呼び出した場合は、この手順を省略できます。

### <a name="file-b-is-opened-by-a-different-editor"></a>ファイル "b" は別のエディターで開かれている

エディター "A" でファイル "b" を開こうとしたときに、これがエディター "B" によって既に開かれている場合は、次の 2 つの異なるシナリオを処理する必要があります。

- ファイル "b" が互換性のあるエディターで開かれている場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> メソッドを使用して、エディター "A" ではファイル "b" に対してドキュメントの編集ロックを登録する必要があります。 エディター "A" でファイル "b" の変更が完了したら、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnregisterDocumentLockHolder%2A> メソッドを使用してドキュメントの編集ロックを登録解除します。

- ファイル "b" が互換性のない方法で開かれている場合、エディター "A" によってファイル "b" を開こうとしたときに失敗させるか、エディター "A" に関連付けられているビューで部分的に開いて、適切なエラー メッセージを表示することができます。 エラー メッセージでは、互換性のないエディターでファイル "b" を閉じて、エディター "A" を使用してファイル "a" を再度開くようにユーザーに指示する必要があります。 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] メソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable2.QueryCloseRunningDocument%2A> を実装して、互換性のないエディターで開いているファイル "b" を閉じるようにユーザーに求めることもできます。 ユーザーがファイル "b" を閉じると、エディター "A" でファイル "a" を開く処理は通常どおり続行されます。

## <a name="additional-document-edit-lock-considerations"></a>ドキュメントの編集ロックに関するその他の考慮事項

エディター "A" がファイル "b" に対してドキュメントの編集ロックを保持する唯一のエディターである場合の動作は、エディター "b" もファイル "b" に対してドキュメントの編集ロックを保持している場合の動作とは異なります。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、**クラス デザイナー** は、関連付けられたコード ファイルの編集ロックを保持しないビジュアル デザイナーの例です。 つまり、ユーザーがデザイン ビューでクラス ダイアグラムを開いていて、関連付けられているコード ファイルが同時に開いている場合に、ユーザーがコード ファイルを変更しても変更を保存していないときは、クラス ダイアグラム (.cd) ファイルへの変更も失われます。 **クラス デザイナー** のみで、コード ファイルに対するドキュメントの編集ロックを保持している場合、ユーザーはコード ファイルを閉じるときに変更を保存するように求められません。 IDE では、ユーザーが **クラス デザイナー** を閉じた後にのみ、変更を保存するようにユーザーに要求します。 保存された変更は両方のファイルに反映されます。 **クラス デザイナー** とコード ファイル エディターの両方で、コード ファイルに対するドキュメントの編集ロックを保持していた場合、コード ファイルまたはフォームのいずれかを閉じるときにユーザーに保存を求めるメッセージが表示されます。 その時点で、保存された変更はフォームとコード ファイルの両方に反映されます。 クラス ダイアグラムの詳細については、「[クラス ダイアグラムの操作 (クラス デザイナー)](../ide/class-designer/designing-and-viewing-classes-and-types.md)」を参照してください。

エディター以外でドキュメントに対して編集ロックを設定する必要がある場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> インターフェイスを実装する必要があることに注意してください。

コード ファイルをプログラムによって変更する UI デザイナーでは、多くの場合、複数のファイルが変更されます。 このような場合、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell2.SaveItemsViaDlg%2A> メソッドでは、 **[次の項目への変更を保存しますか?]** ダイアログ ボックスを使用して 1 つ以上のドキュメントの保存を処理します。

## <a name="see-also"></a>関連項目

- [実行中のドキュメント テーブル](../extensibility/internals/running-document-table.md)
- [永続性と実行中のドキュメント テーブル](../extensibility/internals/persistence-and-the-running-document-table.md)
