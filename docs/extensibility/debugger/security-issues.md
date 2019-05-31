---
title: セキュリティの問題 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- security [Debugging SDK]
- debugging [Debugging SDK], security
ms.assetid: d6ffff0a-afb4-4f38-86d8-476c881c4e4b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4dc31022611d7148d2cb52182b2a10336215afdc
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345614"
---
# <a name="security-issues"></a>セキュリティの問題
Visual Studio を使用してプログラムをデバッグするために必要なアクセス許可は、開発者がプログラムの実行に必要なものと同じです。 これは、ほとんどの場合、リモート デバッグが含まれます。 インターネット インフォメーション サービスなどの他のサービスに関連するいくつかの状況より高いレベルのアクセス許可を必要があります。

 Visual Studio の実行中に、プロセス デバッグ マネージャー (PDM) は、ローカル コンピューター上のデバッグ プロセスを追跡します。 リモートでというプログラム*msvsmon.exe*リモート デバッグを処理し、PDM を使用できるようにするために開発者が開始します。 (*msvsmon.exe*サービスではないと、そのコンピューターにリモート デバッグを有効にするのには手動で開始する必要があります)。ときに Visual Studio (または*msvsmon.exe*) が実行されていないプロセスが追跡されなかったデバッグします。

 開発者は、特別なアクセス許可なしで開始したプログラムをデバッグできます。 開発者は、その他の人が同じセキュリティ グループのメンバーである場合は、他のユーザーによって開始されたプロセスをデバッグもできます。 また、リモート デバッグを有効にするのには、リモート コンピューターに必要なファイルをコピーし、起動にのみ必要な*msvsmon.exe*します。 詳細については、次を参照してください。[リモート デバッグ](../../debugger/remote-debugging.md)します。

## <a name="see-also"></a>関連項目
- [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)
- [プロセス デバッグ マネージャー](../../extensibility/debugger/process-debug-manager.md)
- [リモート デバッグ](../../debugger/remote-debugging.md)
