---
title: MSBuild 16.0 の新機能 | Microsoft Docs
description: MSBuild 16.0 で変更された機能、更新された機能、およびプロパティについて説明し、リリース ノートへのリンクを示します。
ms.custom: SEO-VS-2020
ms.date: 03/11/2019
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: cdfb552c53a40b6ad2f2349556396475926900be
ms.sourcegitcommit: 9cb0097c33755a3e5cbadde3b0a6e9e76cee727d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2021
ms.locfileid: "109848254"
---
# <a name="whats-new-in-msbuild-160"></a>MSBuild 16.0 の新機能

この記事では、MSBuild 16.0 で更新された機能とプロパティについて説明します。 詳細なリリース ノートについては、「[MSBuild 16.0](https://github.com/microsoft/msbuild/releases/tag/v16.0.461.62831)」をご覧ください。

## <a name="changed-path"></a>変更されたパス

 MSBuild は Visual Studio の各バージョンの *\Current* フォルダーにインストールされ、実行可能ファイルは *\Bin* サブフォルダーにインストールされます。 たとえば、Visual Studio 2019 Community でインストールされた *MSBuild.exe* へのパスは *C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\MSBuild\Current\Bin\MSBuild.exe* です。次の PowerShell モジュールを使用して MSBuild を配置することもできます: [vssetup.powershell](https://github.com/Microsoft/vssetup.powershell)。

## <a name="changed-properties"></a>変更されたプロパティ

 新しいバージョン番号に伴い、次の MSBuild プロパティが更新されました。

- `MSBuildToolsVersion`: このバージョンのツールでは "Current" になります。 アセンブリのバージョンは、Visual Studio 2017 と同じ (15.1.0.0) です。

- `VisualStudioVersion`: このバージョンのツールでは "16.0" になります。

## <a name="change-waves"></a>流れの変化

MSBuild 16.8 からは、破壊的な可能性のある特定の MSBuild の変更をオプトアウトするかどうかを選択できます。 「[変更ウェーブ](change-waves.md)」を参照してください。

## <a name="updates"></a>更新

MSBuild (および Visual Studio) では、.NET Framework 4.7.2 が対象とされるようになりました。 MSBuild API の新しい機能を使用したい場合は、ご利用のアセンブリもアップグレードする必要があります。ただし、既存のコードは引き続き機能します。

## <a name="see-also"></a>関連項目

- [MSBuild](../msbuild/msbuild.md)
