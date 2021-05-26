---
title: 実験用インスタンス | Microsoft Docs
description: Visual Studio SDK で、テストされていないアプリケーションをデバッグ モードで実行するための実験用領域を提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- experimental builds
- VSPackages, experimental builds
- VSIP, experimental builds
ms.assetid: ead0df4e-6f88-4b42-9297-581b7902f050
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: aefac4efc706d195d8471952da3914d35d27ddc2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055883"
---
# <a name="the-experimental-instance"></a>実験用インスタンス
テストされていないアプリケーションによって Visual Studio 開発環境が変更されるのを防ぐため、VSSDK には実験に使用できる実験用領域が用意されています。 新しいアプリケーションの開発には Visual Studio を通常どおり使用しますが、それらの実行にはこうした実験用インスタンスを使用します。

 VSIX パッケージが含まれているすべてのアプリケーションで、Visual Studio の実験用インスタンスをデバッグ モードで起動します。

 特定のソリューション以外で Visual Studio の実験用インスタンスを開始する場合は、コマンド ウィンドウで次のコマンドを実行します。

 " *\<Visual studio installation path>* \Common7\IDE\devenv.exe" /RootSuffix Exp

> [!NOTE]
> 実験用インスタンスは、`<version number>Exp` および `<version number>Exp_Config` ノードの下にあるレジストリに書き込まれます。 たとえば、Visual Studio 2015 の実験用のレジストリ領域は以下のとおりです
>
> `HKCU\Software\Microsoft\VisualStudio\14.0Exp` および `HKCU\Software\Microsoft\VisualStudio\14.0Exp_Config`

 拡張機能の開発中は、実験用インスタンスで実行することをお勧めします。 拡張機能をデプロイするときは、開発用インスタンスで実行されます。 アプリケーションの登録の詳細については、「[VSPackage の登録](../extensibility/internals/registering-vspackages.md)」をご覧ください。
