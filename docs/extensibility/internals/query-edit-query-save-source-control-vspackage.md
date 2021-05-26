---
title: クエリの編集とクエリの保存 (ソース管理 VSPackage) | Microsoft Docs
description: Query-Edit Query-Save イベントの役割と、これらがソース管理 VSPackage によって処理されるしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- QEQS events
- Query Edit Query Save events
- source control packages, Query Edit Query Save events
ms.assetid: c360d2ad-fe42-4d65-899d-d1588cc8a322
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9295644a07a1840cd4874b8bfff298ad9d46c928
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060914"
---
# <a name="query-edit-query-save-source-control-vspackage"></a>クエリの編集とクエリの保存 (ソース管理 VSPackage)
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] エディターでは、Query Edit Query Save (QEQS) イベントをブロードキャストできます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ソース管理スタブでは、QEQS イベントの受信者になるように QEQS サービスを実装します。 これらのイベントは、その後、現在アクティブなソース管理 VSPackage に委任されます。 アクティブなソース管理 VSPackage では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> とそのメソッドを実装します。 通常、`IVsQueryEditQuerySave2` インターフェイスのメソッドは、ドキュメントが最初に編集される直前と、ドキュメントが保存される直前に呼び出されます。

## <a name="queryeditquerysave-events"></a>QueryEditQuerySave イベント
 ソース管理 VSPackage では、`IVsQueryEditQuerySave2` インターフェイスと必要なメソッドを実装して、QEQS イベントを処理する必要があります。 VSPackage で最低限実装する必要がある 2 つのメソッドについて、以下に簡単に説明します。 実際の実装は、ソース管理モデルのロジックに従っている必要があります。

### <a name="queryeditfiles-method"></a>QueryEditFiles メソッド
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> は、プロジェクトまたはエディターでファイルを変更する必要があるときに呼び出します。 このメソッドは、ファイルが変更される "*前*" と、ファイルが保存されるときに呼び出すのが理想的です。 このメソッドを呼び出すと、`IVsQueryEditQuerySave2::QueryEditFiles` メソッドによって、指定したファイルがソース管理下にあるかどうか、チェックアウトする必要があるかどうか、それらを再読み込みできるかどうかがチェックされます。 事情によりファイルを編集できない場合は、`IVsQueryEditQuerySave2::QueryEditFiles` メソッドで、呼び出し元のプログラムに対して編集をキャンセルするように指示します。 呼び出し元で呼び出しモードを指定することもできます。 "サイレント" モードでは、UI が表示されない場合にのみ、このメソッドでアクションを実行します。 UI が避けられない場合は、問題を示すフラグを返す必要があります。

 このメソッドはトランザクション方式で動作します。つまり、1 つのファイルで編集がキャンセルされた場合、すべてのファイルで編集がキャンセルされます。 逆に、編集が許可された場合は、すべてのファイルで許可されます。 このメソッドで特定のファイル セットに対して 1 回の編集を許可した場合は、同じファイル セットに対する後続の呼び出しで常に編集を許可する必要があります。 この編集許可のループは、ファイルが閉じられ、保存され、再読み込みされるまで、属性 (プロパティ) が変更されるまで、またはソース管理パッケージが変更されるまで、続行されます。 `IVsQueryEditQuerySave2::QueryEditFiles` メソッドの実装で考慮すべきケースとして、複数のファイル、特別なファイル、ユーザーからのキャンセル、メモリ内の編集などがあります。

### <a name="querysavefiles-method"></a>QuerySaveFiles メソッド
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> は、プロジェクトまたはエディターでファイル セットを保存する必要があるときに呼び出されます。 `IVsQueryEditQuerySave2::QuerySaveFiles` メソッドを呼び出すと、指定したファイルが読み取り専用かどうか、およびそれらがソース管理下にあるかどうかがチェックされます。 ファイルをチェックアウトする必要がある場合は、呼び出しがソース管理パッケージに委任されます。 事情によりファイルを保存できない場合は、`IVsQueryEditQuerySave2::QuerySaveFiles` メソッドで、保存をキャンセルするようにエディターに指示する必要があります。 `IVsQueryEditQuerySave2::QueryEditFiles` メソッドと同様に、呼び出し元で呼び出しモードを指定することもできます。 "サイレント" モードでは、UI が表示されない場合にのみ、このメソッドでアクションを実行します。 UI が避けられない場合は、問題を示すフラグを返す必要があります。

 このメソッドはトランザクション方式で動作する必要があります。つまり、1 つのファイルで保存がキャンセルされた場合、すべてのファイルで保存がキャンセルされます。 逆に、保存が許可された場合は、すべてのファイルで許可される必要があります。 `IVsQueryEditQuerySave2::QueryEditFiles` メソッドと同様に、`IVsQueryEditQuerySave2::QuerySaveFiles` メソッドの実装で考慮すべきケースとして、複数のファイル、特別なファイル、ユーザーからのキャンセル、メモリ内の編集などがあります。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
