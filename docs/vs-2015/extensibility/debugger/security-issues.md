---
title: セキュリティの問題 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- security [Debugging SDK]
- debugging [Debugging SDK], security
ms.assetid: d6ffff0a-afb4-4f38-86d8-476c881c4e4b
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 874231333c87020c126eac4c066d53512ba0bbc9
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58962354"
---
# <a name="security-issues"></a>セキュリティ上の問題
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio を使用してプログラムをデバッグするために必要なアクセス許可は、開発者がプログラムを実行する必要があるものと同じです。 これは、ほとんどの状況が (インターネット インフォメーション サービスなどの他のサービスに関連するいくつかの状況はより高いレベルのアクセス許可である必要があります) のリモート デバッグが含まれます。  
  
 Visual Studio の実行中に、プロセス デバッグ マネージャー (PDM) は、ローカル コンピューター上のデバッグ プロセスを追跡します。 リモートでのリモート デバッグを処理し、PDM を使用できるようにするために開発者 msvsmon.exe と呼ばれるプログラムを起動します。 (その msvsmon.exe がサービスではないと、そのコンピューターにリモート デバッグを有効にするのには手動で開始する必要がありますに注意してください)。Visual Studio (または msvsmon.exe) が実行されていない場合は、デバッグ プロセスが追跡ありません。  
  
 つまり、開発者が自分が特別なアクセス許可なしで開始されたプログラムをデバッグできます。 開発者は、その他の人が同じセキュリティ グループのメンバーである場合は、他のユーザーによって開始されたプロセスをデバッグもできます。 リモート デバッグを有効にする必要があるだけで、必要なをコピーするファイルをリモート コンピューターし、msvsmon.exe を開始し、(を参照してください[設定 Up the Remote Tools のデバイスで](http://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)の詳細)。  
  
## <a name="see-also"></a>関連項目  
 [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)   
 [プロセス デバッグ マネージャー](../../extensibility/debugger/process-debug-manager.md)   
 [デバイスのリモート ツールのセットアップ](http://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)
