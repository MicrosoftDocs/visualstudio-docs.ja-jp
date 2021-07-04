---
title: Security
description: セキュリティ コンセプトと、安全なアプリケーションの効果的開発に役立つセキュリティ機能について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/01/2018
ms.topic: conceptual
helpviewer_keywords:
- security [Visual Studio], applications
- application design, securability
ms.assetid: 7d32c4cf-8bec-4307-a2a8-42f0ceddf3eb
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f3dcd034a76fbc371c95a2bbf386687830e3b63d
ms.sourcegitcommit: 63cb90e8cea112aa2ce8741101b309dbc709e393
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2021
ms.locfileid: "110687653"
---
# <a name="secure-applications"></a>セキュリティで保護されたアプリケーション

セキュリティについては、設計から配置まで、アプリケーション開発のあらゆる段階で考慮する必要があります。 まず、Visual Studio をできるだけ安全に実行します。 [ユーザー アクセス許可](../ide/user-permissions-and-visual-studio.md)に関するページを参照してください。

安全なアプリケーションを効果的に開発するためには、セキュリティの概念と、開発対象となるプラットフォームのセキュリティ機能について、基本事項を理解しておく必要があります。 さらに、安全なコーディング技法を身に付ける必要もあります。

## <a name="code-for-security"></a>セキュリティに配慮したコード

セキュリティ脆弱性の原因となるコーディング エラーのほとんどは、ユーザー入力に対する根拠のない仮定や、開発対象のプラットフォームに対する不十分な知識に起因しています。

- 「[安全なコーディングのガイドライン](/dotnet/standard/security/secure-coding-guidelines)」では、セキュリティ システムと連携するよう .NET コードを設計するさまざまな方法を説明します。
- 「[C++ のセキュリティ ベスト プラクティス](/cpp/top/security-best-practices-for-cpp)」では、C++ 開発者向けのセキュリティ ツールと推奨事項の情報を説明します。

## <a name="build-for-security"></a>セキュリティに配慮したビルド

セキュリティはビルド プロセスでも重要な考慮事項です。 いくつかの追加手順で、展開するアプリのセキュリティを改善し、不正なリバース エンジニアリング、なりすましなどの攻撃を防ぐことができます。

- [Dotfuscator](dotfuscator/index.md) は無料で、.NET アセンブリをリバース エンジニアリングや許可されていないデバッグなどの許可されていない使用から保護するのに役立ちます。
- [厳密な名前の署名](managing-assembly-and-manifest-signing.md)を使用すると、ソフトウェア コンポーネントを一意に識別し、名前のなりすましを防ぐことができます。

## <a name="see-also"></a>関連項目

- [.NET でのセキュリティ](/dotnet/standard/security/index)
- [Azure のセキュリティ](/azure/security/)
- [Windows 10 Mobile のセキュリティ ガイド](/windows/security/threat-protection/windows-10-mobile-security-guide)
- [Apache Cordova プラットフォームのセキュリティ機能](/previous-versions/visualstudio/cross-platform/tools-for-cordova/security/best-practices?view=toolsforcordova-2017&preserve-view=true)
- [ASP.NET Core のセキュリティ](/aspnet/core/security/?view=aspnetcore-2.1&preserve-view=true)
- [Windows フォームのセキュリティ](/dotnet/framework/winforms/windows-forms-security)
