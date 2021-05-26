---
title: VSPackage のセキュリティのベスト プラクティス | Microsoft Docs
description: Visual Studio アプリケーションのセキュリティとデプロイの基本単位である VSPackage のセキュリティのベスト プラクティスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- security [Visual Studio SDK]
- security best practices, VSPackages
- best practices, security
ms.assetid: 212a0504-cf6c-4e50-96b0-f2c1c575c0ff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cca66d6c1fce0deb8103a7d626c16a4e81bc7b5f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086210"
---
# <a name="best-practices-for-security-in-vspackages"></a>VSPackage のセキュリティのベスト プラクティス
コンピューターに [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] をインストールするには、管理者資格情報を持つコンテキストで実行している必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] アプリケーションのセキュリティとデプロイの基本単位は [VSPackage](../../extensibility/internals/vspackages.md) です。 VSPackage は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] を使用して登録する必要がありますが、これには管理者の資格情報も必要です。

 管理者は、レジストリとファイル システムに書き込み、任意のコードを実行するための完全なアクセス許可を持っています。 VSPackage を開発、デプロイ、またはインストールするには、これらのアクセス許可を持っている必要があります。

 インストールが完了するとすぐに、VSPackage は完全に信頼されます。 この高いレベルのアクセス許可が VSPackage に関連付けられているため、悪意のある VSPackage を誤ってインストールする可能性があります。

 ユーザーは、信頼できるソースからのみ VSPackage をインストールする必要があります。 VSPackage を開発する企業は、改ざんが防止されていることをユーザーに保証するために、厳密に名前を付けて署名する必要があります。 VSPackage を開発する企業は、Web サービスやリモート インストールなどの外部依存関係を調べて、セキュリティ上の問題を評価し、修正する必要があります。

 詳細については、[.NET Framework の安全なコーディングのガイドライン](/previous-versions/visualstudio/visual-studio-2008/d55zzx87(v=vs.90))に関するページを参照してください。

## <a name="see-also"></a>関連項目
- [アドインのセキュリティ](/previous-versions/1326zbk3(v=vs.140))
- [DDEX のセキュリティ](/previous-versions/bb163703(v=vs.140))