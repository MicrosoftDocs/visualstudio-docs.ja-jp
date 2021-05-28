---
title: IWefDebuggingSupport インターフェイス
description: Visual Studio などのデバッグ環境を使用して Microsoft Office アプリケーションのデバッグを容易にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9fc319429414c8976d748a30ecdd1e164ce22b63
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99962263"
---
# <a name="iwefdebuggingsupport-interface"></a>IWefDebuggingSupport インターフェイス
  Office 用アプリのデバッグを容易にするために、Visual Studio などのデバッグ環境によって実装されます。 Word や Excel などの Office アプリケーションでは、Visual Studio からこのインターフェイスを取得した後、デバッグ セッション中に特定の時点でインターフェイスのメソッドが呼び出されます。

## <a name="syntax"></a>構文

```csharp
[
    uuid(ccaf1a90-ce1c-4199-9cd6-b40c5c57a671),
    oleautomation
]
interface IWefDebuggingSupport : IUnknown
{
    HRESULT SetWefProcessId(
        [in] DWORD dwProcessId);
    HRESULT GetAutoInsertExtensions(
        [out, retval] SAFEARRAY(BSTR)* psaExtensionNames);
}
```

## <a name="methods"></a>メソッド
 次の表は、IWefDebuggingSupport インターフェイスで定義されるメソッドを示しています。

|名前|説明|
|----------|-----------------|
|[GetAutoInsertExtensions メソッド](../vsto/getautoinsertextensions-method.md)|デバッグの間に自動的に挿入される Office 用アプリに関する情報を取得します。|
|[SetWefProcessId メソッド](../vsto/setwefprocessid-method.md)|Web Extensions Framework (WEF) コンテンツを実行するプロセス識別子を提供します。|
