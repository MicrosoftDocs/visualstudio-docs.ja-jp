---
title: '方法: Office のプライマリ相互運用機能アセンブリをインストールする'
description: Microsoft Office のインストール時に、Office のプライマリ相互運用機能アセンブリ (PIA) をインストールする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- primary interop assemblies [Office development in Visual Studio], installing
- Office primary interop assemblies, installing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 432b2a74eb7ea4753cd110956c9dc9313e1a5d6e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99934820"
---
# <a name="how-to-install-office-primary-interop-assemblies"></a>方法: Office のプライマリ相互運用機能アセンブリをインストールする
  Microsoft Office のインストール時に、Office のプライマリ相互運用機能アセンブリ (PIA) をインストールします。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="to-install-the-pias-when-you-install-office"></a>Office のインストール時に PIA をインストールするには

1. .NET Framework のバージョンが 2.0 以降であることを確認します。

2. Microsoft Office をインストールします。このとき、拡張するアプリケーションの **.NET プログラミング サポート** 機能が選択されていることを確認します (この機能は既定のインストールに含まれています)。

    > [!WARNING]
    > 既定では、ソリューションのビルド時に、PIA がそのソリューションに埋め込まれるため、VSTO アドインまたはカスタマイズを使用するための前提条件として、PIA をユーザーに配布する必要はありません。

## <a name="see-also"></a>関連項目
- [Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)
- [方法: プライマリ相互運用機能アセンブリを利用して Office アプリケーションを使用する](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [方法: Office ソリューションを開発できるようにコンピューターを構成する](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [方法: Visual Studio Tools for Office の再頒布可能なランタイムをインストールする](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [はじめに &#40;Visual Studio での Office 開発&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
