---
title: '方法: ウィンドウへのオートメーションの提供 | Microsoft Docs'
description: Microsoft.VisualStudio.Shell.Interop のメソッドを使用して、Visual Studio でドキュメントとツールのウィンドウにオートメーションを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- automation [Visual Studio SDK], tool windows
- tool windows, automation
ms.assetid: 512ab2a4-7987-4912-8f40-8804bf66f829
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 774b32dc1554fb6d6466be7e915fbaeea8185798
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078748"
---
# <a name="how-to-provide-automation-for-windows"></a>方法: ウィンドウへのオートメーションの提供

ドキュメントとツールのウィンドウにオートメーションを提供できます。 ウィンドウでオートメーション オブジェクトを使用できるようにしたい一方で、環境で既製のオートメーション オブジェクトが提供されていない場合は、タスク リストを使用する場合と同様に、常にオートメーションを提供することをお勧めします。

## <a name="automation-for-tool-windows"></a>ツール ウィンドウでのオートメーション

環境では、次の手順で説明するように、標準の <xref:EnvDTE.Window> オブジェクトを返すことによって、ツール ウィンドウにオートメーションが提供されます。

1. 環境から、[_VSFPROPID.VSFPROPID_ExtWindowObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ExtWindowObject>) を `VSFPROPID` パラメーターとして指定して <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> メソッドを呼び出し、`Window` オブジェクトを取得します。

2. 呼び出し元が <xref:EnvDTE.Window.Object%2A> を通じてツール ウィンドウ用の VSPackage 固有のオートメーション オブジェクトを要求すると、環境では `IExtensibleObject`、<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>、または `IDispatch` インターフェイスに対し `QueryInterface` が呼び出されます。 `IExtensibleObject` と `IVsExtensibleObject` の両方によって <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject.GetAutomationObject%2A> メソッドが提供されます。

3. その後、環境で `NULL` を渡す `GetAutomationObject`メソッドが呼び出されたら、VSPackage 固有のオブジェクトを渡して応答します。

4. `IExtensibleObject` および `IVsExtensibleObject` に対する `QueryInterface` の呼び出しが失敗した場合、環境では `IDispatch` に対して `QueryInterface` が呼び出されます。

## <a name="automation-for-document-windows"></a>ドキュメント ウィンドウでのオートメーション

エディターでは、`IExtensibleObject` インターフェイスを実装して `GetAutomationObject` に応答することによって、<xref:EnvDTE.Document> オブジェクトの独自の実装を含めることができますが、標準の <xref:EnvDTE.Document> オブジェクトは環境からも使用できます。

また、エディターでは、`IVsExtensibleObject` または `IExtensibleObject` インターフェイスを実装することによって、<xref:EnvDTE.Document.Object%2A> メソッドを通じて取得される VSPackage 固有のオートメーション オブジェクトを提供でき ます。 [VSSDK サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)は、RTF ドキュメント固有のオートメーション オブジェクトの提供に役立っています。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>
