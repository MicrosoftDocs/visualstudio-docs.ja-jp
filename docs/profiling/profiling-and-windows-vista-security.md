---
title: プロファイルと Windows Vista のセキュリティ | Microsoft Docs
ms.custom: ''
ms.date: 11/02/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools,security
- performance tools, security
ms.assetid: 842112fc-b886-4801-8cd7-a25b314b0393
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 767210a934753dd85b22728813d7608618a2b8d3
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2018
ms.locfileid: "51220658"
---
# <a name="profiling-and-windows-vista-security"></a>プロファイルと Windows Vista のセキュリティ

コンピューターの管理者が使用可能にした [!INCLUDE[wiprlhext](../debugger/includes/wiprlhext_md.md)] ユーザー アクセス許可の設定に応じて、個々のユーザーは、コンピューター上でプロセスをプロファイリングするためのセキュリティ アクセス許可を持っている場合があります。 次の例では、考えられるユーザーごとの違いについて説明します。

- 管理者がドライバーとサービスが起動するように設定しているときには、一部のユーザーが高度なプロファイリング機能にアクセスできることがあります。

- ドメイン ユーザーはサンプルのプロファイリングにのみアクセスできる場合があります。

- 一部のユーザーが他のすべてのユーザーに対してプロファイリングへのアクセスを拒否することがあります。

  詳細については、「[VSPerfCmd](../profiling/vsperfcmd.md)」の ADMIN オプションを参照してください。

## <a name="cross-session-profiling"></a>セッション間プロファイリング

*セッション間プロファイリング*は、別のユーザー セッションで実行しているプロセスをプロファイリングする機能です。 たとえば、サービスのほとんどはセッション 0 で実行され、ユーザーはセッション 0 で直接実行できません。 パフォーマンス エクスプローラーのツールバーで **[プロセスにアタッチ]** ボタン、または VSPerfCmd コマンドライン ツールの `/attach` オプションを使用して、さまざまなユーザー セッションでのほとんどのプロセスをプロファイリングすることができます。

プロセス間のプロファイルの表示オプションを設定すると、使用できるプロセスの一覧が表示できます。 これらのオプションは、**[プロセスにアタッチ]** を選択すると表示される **[プロセスにアタッチ]** ウィンドウで利用できます。

- **全ユーザーのプロセスを表示する**

  このオプションを選択していない場合、一覧には、現在のユーザーによって所有されているプロセスのみが表示されます。 選択している場合、すべてのユーザーのプロセスが一覧表示されます。

- **すべてのセッションのプロセスを表示**

  このオプションを選択していない場合、一覧には、現在のセッションのプロセスが表示されます。 選択している場合、すべてのセッションのプロセスが一覧表示されます。

## <a name="see-also"></a>関連項目

- [概要](../profiling/overviews-performance-tools.md)
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [方法: 実行中のプロセスにアタッチする](/previous-versions/visualstudio/visual-studio-2010/c6wf8e4z\(v\=vs.100\))
