---
title: セキュリティの問題 | Microsoft Docs
description: リモート デバッグや、他のサービスが関係する状況など、Visual Studio を使用してプログラムをデバッグするために必要なアクセス許可について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- security [Debugging SDK]
- debugging [Debugging SDK], security
ms.assetid: d6ffff0a-afb4-4f38-86d8-476c881c4e4b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1994a4a95d005edf4a71df3a1bb899522ecec137
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070428"
---
# <a name="security-issues"></a>セキュリティの問題
Visual Studio を使用してプログラムをデバッグするには、開発者がプログラムを実行する場合と同じアクセス許可が必要です。 これには、ほとんどの状況でのリモート デバッグが含まれます。 インターネット インフォメーション サービスなど、他のサービスが関係する状況の中には、より高いレベルの権限が必要なものがあります。

 Visual Studio の実行中にプロセス デバッグ マネージャー (PDM) は、ローカル コンピューター上のデバッグ プロセスを追跡します。 リモートデバッグを処理し、PDM を使用できるようにするために開発者は、*msvsmon.exe* と呼ばれるプログラムをリモートで起動します (*msvsmon.exe* はサービスではないため、手動で起動して、そのコンピューターでリモート デバッグを有効にする必要があります)。Visual Studio (または *msvsmon.exe*) が実行されていない場合は、プロセスがデバッグのために追跡されません。

 開発者は、特別なアクセス許可なしで開始したプログラムをデバッグできます。 他のユーザーによって開始されたプロセスも、そのユーザーが、同じセキュリティ グループのメンバーである場合にはデバッグできます。 また、必要なファイルをリモート コンピューターにコピーして *msvsmon.exe* を開始するだけで、リモート デバッグを有効にすることができます。 詳細については、「[リモート デバッグ](../../debugger/remote-debugging.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)
- [プロセス デバッグ マネージャー](../../extensibility/debugger/process-debug-manager.md)
- [リモート デバッグ](../../debugger/remote-debugging.md)
