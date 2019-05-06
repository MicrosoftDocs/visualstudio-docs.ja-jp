---
title: CA2001:問題が発生する可能性のあるメソッドは呼び出しません
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2001
- AvoidCallingProblematicMethods
helpviewer_keywords:
- CA2001
- AvoidCallingProblematicMethods
ms.assetid: 19db8edb-31ce-441c-b0de-a0f2746155b7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1abef0067a58225eea6110d4cc2f7257bc605463
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62808388"
---
# <a name="ca2001-avoid-calling-problematic-methods"></a>CA2001:問題が発生する可能性のあるメソッドは呼び出しません

|||
|-|-|
|TypeName|AvoidCallingProblematicMethods|
|CheckId|CA2001|
|カテゴリ|Microsoft.Reliability|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因

メンバーが危険性または問題のあるメソッドを呼び出します。

## <a name="rule-description"></a>規則の説明

不要なおよび危険のメソッドの呼び出しを回避します。 この規則違反は、メンバーは、次のメソッドのいずれかを呼び出すときに発生します。

|メソッド|説明|
|------------|-----------------|
|<xref:System.GC.Collect%2A?displayProperty=fullName>|GC を呼び出しています。収集は、アプリケーションのパフォーマンスに大きく影響し、必要はほとんどありません。 詳細については、次を参照してください。 [Rico Mariani のパフォーマンスに関するニュース](http://go.microsoft.com/fwlink/?LinkId=169256)msdn ブログ エントリ。|
|<xref:System.Threading.Thread.Resume%2A?displayProperty=fullName><br /><br /> <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName>|Thread.Suspend および Thread.Resume が、予期しない動作のために使用されなくなりました。  他のクラスを使用して、<xref:System.Threading>名前空間など<xref:System.Threading.Monitor>、<xref:System.Threading.Mutex>と<xref:System.Threading.Semaphore>スレッドを同期またはリソースを保護します。|
|<xref:System.Runtime.InteropServices.SafeHandle.DangerousGetHandle%2A?displayProperty=fullName>|DangerousGetHandle メソッドでは、無効なハンドルを返すことができますので、セキュリティ リスクが生じます。 参照してください、<xref:System.Runtime.InteropServices.SafeHandle.DangerousAddRef%2A>と<xref:System.Runtime.InteropServices.SafeHandle.DangerousRelease%2A>DangerousGetHandle メソッドを安全に使用する方法の詳細についてのメソッド。|
|<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>|これらのメソッドは、予期しない場所からアセンブリを読み込むことができます。 たとえば、Suzanne Cook の .NET CLR のノートのブログ投稿を参照して[LoadFile vs します。LoadFrom](http://go.microsoft.com/fwlink/?LinkId=164450)と[バインド コンテキストを選択する](http://go.microsoft.com/fwlink/?LinkId=164451)アセンブリを読み込む方法についてはします。|
|[CoSetProxyBlanket](http://go.microsoft.com/fwlink/?LinkID=169250) (Ole32)<br /><br /> [CoInitializeSecurity](http://go.microsoft.com/fwlink/?LinkId=169255) (Ole32)|ユーザー コードがマネージ プロセスで実行を開始するのには遅すぎます CoSetProxyBlanket を確実に呼び出すです。 共通言語ランタイム (CLR) は、次の位置からユーザーの P/invoke を妨げる可能性のある初期化アクションを実行します。<br /><br /> マネージ アプリケーションの CoSetProxyBlanket を呼び出すを持っている場合は、ネイティブ コード (C++) の実行可能ファイルを使用して、プロセスを開始し、CoSetProxyBlanket を呼び出すネイティブ コードでのプロセスでマネージ コード アプリケーションを起動ことを勧めします。 (するランタイムのバージョン番号を指定してください)。|

## <a name="how-to-fix-violations"></a>違反の修正方法

このルールの違反を修正するには、削除するか、危険性または問題のあるメソッドの呼び出しを置き換えます。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。

問題のある方法の代替手段が使用できない場合にのみ、この規則からのメッセージを抑制する必要があります。

## <a name="see-also"></a>関連項目

- [信頼性の警告](../code-quality/reliability-warnings.md)