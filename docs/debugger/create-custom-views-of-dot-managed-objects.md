---
title: 管理オブジェクトのカスタムビューを作成する |Microsoft Docs
ms.date: 01/08/2019
ms.topic: conceptual
f1_keywords:
- vs.debug.data.elements
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- data types, custom
- custom data types
- managed code, custom data types
- autoexp.dat file
- mcee_cs.dat file
- debugger, expanding data types
- mcee_mc.dat file
ms.assetid: 9969e9b2-9008-4729-8a14-0d6deaa61576
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 4649ac11daa062089d2916a5d5d0a331e4d74272
ms.sourcegitcommit: 1507baf3a336bbb6511d4c3ce73653674831501b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72349453"
---
# <a name="create-custom-views-of-managed-objects-c-visual-basic-f-ccli"></a>管理オブジェクト (C#、Visual Basic、 F# C++/cli) のカスタムビューを作成する
Visual Studio でデバッガーの変数ウィンドウにデータ型を表示する方法をカスタマイズできます。

## <a name="attributes"></a>属性

、 C#、Visual Basic F# C++ (C++/cli コードのみ) では、<xref:System.Diagnostics.DebuggerTypeProxyAttribute>、<xref:System.Diagnostics.DebuggerDisplayAttribute>、および @no__t を使用して、カスタムデータの展開を追加できます。

.NET Framework 2.0 コードでは、Visual Basic はデバッガ参照可能属性をサポートしていません。 この制限は、.NET Framework の新しいバージョンで解除されています。

## <a name="visualizers"></a>ビジュアライザー

マネージド データ型を表示するには、ビジュアライザーを記述します。 詳細については、「[方法: ビジュアライザーを記述](/visualstudio/debugger/create-custom-visualizers-of-data)する」を参照してください。

> [!NOTE]
> コードC++の場合、「[デバッガーでのオブジェクトのカスタムビューの作成C++ ](/visualstudio/debugger/create-custom-views-of-native-objects)」で説明されているように、Natvis フレームワークを使用してカスタムデータ型の展開を追加できます。

## <a name="see-also"></a>参照

- [デバッガ Display 属性を使用して、表示する内容をデバッガーに通知します](../debugger/using-the-debuggerdisplay-attribute.md)
- [Debugger Typeproxy 属性を使用して表示する型をデバッガーに通知する](../debugger/using-debuggertypeproxy-attribute.md)
- [ウォッチ ウィンドウと [クイック ウォッチ] ウィンドウ](../debugger/watch-and-quickwatch-windows.md)
- [デバッガー表示属性によるデバッグ機能の拡張](/dotnet/framework/debug-trace-profile/enhancing-debugging-with-the-debugger-display-attributes)
