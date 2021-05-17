---
title: カスタム デバッグ エンジンのデバッグ | Microsoft Docs
description: デバッグ エンジンが COM 規則に従って自身をクラス ファクトリとして登録する方法と、レジストリを介して Visual Studio に登録する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, registering
ms.assetid: 9984cd3d-d34f-4662-9ace-31766499abf5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 04e4e8de875cb66ed285e610950baa1c5bf4ef3f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070662"
---
# <a name="register-a-custom-debug-engine"></a>カスタム デバッグ エンジンを登録する
デバッグ エンジンは、COM 規則に従って自身をクラス ファクトリとして登録し、Visual Studio レジストリ サブキーを使用して Visual Studio に登録する必要があります。

> [!NOTE]
> デバッグ エンジンの登録方法の例は、TextInterpreter サンプルにあります。このサンプルは、「[チュートリアル: ATL COM を使用したデバッグ エンジンの構築](/previous-versions/bb147024(v=vs.90))」の一部として作成されています。

## <a name="dll-server-process"></a>DLL サーバー プロセス
 デバッグ エンジンは、通常、それ自体の DLL で COM サーバーとして設定されます。 そのため、デバッグ エンジンは、そのクラス ファクトリの CLSID を COM に登録して、Visual Studio がアクセスできるようにする必要があります。 次に、デバッグ エンジンは、それ自体を Visual Studio に登録して、デバッグ エンジンがサポートするすべてのプロパティ (メトリックとも呼ばれます) を確立する必要があります。 Visual Studio レジストリ サブキーに書き込まれるメトリックの選択は、デバッグ エンジンがサポートする機能によって異なります。

 [デバッグ用 SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) は、デバッグ エンジンの登録に必要なレジストリの場所だけでなく、*dbgmetric.lib* ライブラリについても説明します。このライブラリには、レジストリ操作を容易にする、C++ 開発者向けの便利な関数と宣言が数多く含まれています。

### <a name="example"></a>例
 次の例 (TextInterpreter サンプルの) では、`SetMetric` 関数 (*dbgmetric.lib* の) を使用してデバッグ エンジンを Visual Studio に登録する方法を示しています。 渡されているメトリックは、*dbgmetric.lib* でも定義されています。

> [!NOTE]
> TextInterpreter は、基本的なデバッグ エンジンです。その他の機能を設定しないため、その登録も行いません。 より完全なデバッグ エンジンには、デバッグ エンジンがサポートしている機能ごとに 1 つずつ、すべての `SetMetric` 呼び出しまたはそれに相当する機能が含まれています。

```
// Define base registry subkey to Visual Studio.
static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0";

HRESULT CTextInterpreterModule::RegisterServer(BOOL bRegTypeLib, const CLSID * pCLSID)
{
    SetMetric(metrictypeEngine, __uuidof(Engine), metricName, L"Text File", false, strRegistrationRoot);
    SetMetric(metrictypeEngine, __uuidof(Engine), metricCLSID, CLSID_Engine, false, strRegistrationRoot);
    SetMetric(metrictypeEngine, __uuidof(Engine), metricProgramProvider, CLSID_MsProgramProvider, false, strRegistrationRoot);

    return base::RegisterServer(bRegTypeLib, pCLSID);
}
```

## <a name="see-also"></a>関連項目
- [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
- [デバッグ用 SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [チュートリアル: ATL COM を使用したデバッグ エンジンの構築](/previous-versions/bb147024(v=vs.90))