---
title: 'エラー: x64 プロセスの混合モードデバッグは Microsoft .NET Framework 4 以上を使用している場合にのみサポートされます。Microsoft Docs'
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.interop_unsupported_x64
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 67b9d1c737e4490195b209abca824b2d6d51176c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72737600"
---
# <a name="error-mixed-mode-debugging-for-x64-processes-is-supported-only-when-using-microsoft-net-framework-4-or-greater"></a>エラー: x64 プロセスの混合モード デバッグは、Microsoft .NET Framework 4 以上を使用している場合にのみサポートされます
64ビットプロセスでネイティブコードとマネージコードの混合コードをデバッグするには .NET Framework バージョン4が必要です。 .NET Framework バージョンが4より前の64ビットプロセスの混合モードデバッグはサポートされていません。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- 次のいずれかの操作を実行します。

  - .NET Framework をバージョン4にアップグレードします。

  - デバッグのため、32 ビット バージョンのアプリケーションをビルドします。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)