---
title: CreateExpInstance ユーティリティ | Microsoft Docs
description: CreateExpInstance ユーティリティについて説明します。これを使用すると、Visual Studio の実験用インスタンス作成や、リセット、削除を行うことができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- experimental builds
- experimental hive
- experimental instance
- createexpinstance
- createexpinst
ms.assetid: 03779774-9401-49ae-997c-0c3ab25ed0d5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d0010c4a98d0ea50ec7feb2f7a379f3c84bc3d53
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056988"
---
# <a name="createexpinstance-utility"></a>CreateExpInstance ユーティリティ
**CreateExpInstance** ユーティリティを使用すると、Visual Studio の実験用インスタンスの作成や、リセット、削除を行うことができます。 実験用インスタンスを使用して、基になる製品を変更せずに Visual Studio の拡張機能のデバッグとテストを行うことができます。

## <a name="syntax"></a>構文

```
CreateExpInstance.exe [/Create | /Reset | /Clean] /VSInstance=VsInstance /RootSuffix=Suffix
```

## <a name="parameters"></a>パラメーター
 **/Create** 実験用インスタンスを作成します。

 **/Reset** 実験用インスタンスを削除した後、新しいインスタンスを作成します。

 **/Clean** 実験用インスタンスを削除します。

 **/VSInstance** コピー対象になる、基の Visual Studio インスタンスが格納されているディレクトリの名前です。

 **/RootSuffix** 実験用インスタンス ディレクトリの名前に追加するサフィックスです。

## <a name="remarks"></a>解説
 Visual Studio の拡張機能を使用しているときに、F5 キーを押して既定の実験用インスタンスを開き、現在の拡張機能をインストールできます。 使用できる実験用インスタンスがない場合、Visual Studio によって、既定の設定を備えるインスタンスが作成されます。

 実験用インスタンスの既定の場所は、Visual Studio のバージョン番号によって異なります。 たとえば、Visual Studio 2015 の場合、場所は *%localappdata%\Microsoft\VisualStudio\14.0Exp \\* です。 ディレクトリの場所にあるすべてのファイルは、そのインスタンスの一部と見なされます。 ディレクトリ名が既定の場所に変更されている場合を除き、追加される別の実験用インスタンスが Visual Studio によって読み込まれることはありません。

 Visual Studio によって実験用インスタンスが開かれているとき、Visual Studio からシステム レジストリにアクセスすることはありません。 これは、レジストリ ハイブの実験用バージョンが使用されていた、以前のバージョンの Visual Studio とは異なります。

 **CreateExpInstance** ユーティリティは、**VsRegEx** ユーティリティに代わるものです。

 次の例では、Visual Studio の既定の実験用インスタンスがリセットされます。

 **CreateExpInstance.exe /Reset /VSInstance=14.0 /RootSuffix=Exp**

## <a name="see-also"></a>関連項目
- [VSPackages](../../extensibility/internals/vspackages.md)
