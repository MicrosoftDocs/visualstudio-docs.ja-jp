---
title: .NET Framework ベースの国際対応アプリケーションの概要
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- strings [Visual Studio], localizing
- Web applications [.NET Framework], globalization
- Windows Forms, globalization
- localization [Visual Studio], culture setting
- fallback resources
- culture, setting
- globalization [Visual Studio], culture setting
- resources [Visual Studio], localization
- localization [Visual Studio], .NET localization model
- Assembly Resource file template
- resources [Visual Studio], fallback system
- international applications [Visual Studio], about international applications
- globalization [Visual Studio], international applications
- ASP.NET, globalization
- resource files, fallback processes
- user interface, culture setting
ms.assetid: b0788993-e62d-4f68-8235-5f87b1d48525
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: fffa31d19a3b65e559800153d935d53e9ea008c6
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55924618"
---
# <a name="introduction-to-international-applications-based-on-the-net-framework"></a>.NET Framework ベースの国際対応アプリケーションの概要

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] での国際対応アプリケーションの作成は 2 つの部分で構成されています。1 つはグローバリゼーションという、異なるカルチャに対応できるアプリケーションを設計するプロセスで、もう 1 つはローカリゼーションという、特定のカルチャに合わせてリソースを翻訳するプロセスです。 各国のユーザーに向けたアプリケーションの設計に関する一般的な情報については、「[推奨される国際対応アプリケーション開発手順](/dotnet/standard/globalization-localization/best-practices-for-developing-world-ready-apps)」を参照してください。

 [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] のローカリゼーション モデルは、アプリケーション コードとフォールバック リソース (アプリケーションが最初に開発されたときに使用された言語の文字列、イメージ、およびその他のオブジェクト) の両方を含むメイン アセンブリで構成されています。 ローカライズされた各アプリケーションには、サテライト アセンブリ (ローカライズされたリソースのみを含むアセンブリ) があります。 メイン アセンブリには常にフォールバック リソースが含まれるため、ローカライズされたサテライト アセンブリでリソースが見つからない場合、<xref:System.Resources.ResourceManager> はそのリソースを階層的に読み込もうとし、最終的にはメイン アセンブリのリソースに戻ります。 リソースのフォールバック システムの詳細については、「[ローカリゼーション用リソースの階層編成](../ide/hierarchical-organization-of-resources-for-localization.md)」を参照してください。

 Microsoft のローカライズされたすべての製品に関する用語集も、ローカリゼーション リソースとして使用するよう考えてください。 この CSV ファイルには、12,000 を超える英語の用語と、最大 59 種類の言語に翻訳された用語が含まれます。 用語集は、「[Microsoft Terminology Translations](http://go.microsoft.com/fwlink/?LinkId=128146)」(Microsoft 用語翻訳) Web ページからダウンロードできます。

 Windows フォーム アプリケーションのプロジェクト システムでは、フォールバックと必要な追加の UI カルチャの両方のリソース ファイルを生成できます。 フォールバック リソース ファイルがメイン アセンブリに組み込まれてから、カルチャ固有のリソース ファイルがサテライト アセンブリ (UI カルチャごとに 1 つ) に組み込まれます。 プロジェクトをビルドすると、リソース ファイルは Visual Studio XML 形式 (.resx) から中間バイナリ形式 (.resources) にコンパイルされ、その後、サテライト アセンブリに埋め込まれます。

 Windows フォームと Web フォームの両方のプロジェクト システムで、アセンブリ リソース ファイル テンプレートを使用してリソース ファイルをビルドし、リソースにアクセスしてプロジェクトをビルドすることができます。 サテライト アセンブリはメイン アセンブリと共に作成されます。

 ローカライズされたアプリケーションの実行時の外観は 2 つのカルチャ値によって決まります  (*カルチャ*とは、ユーザーの言語、環境、および文化的な慣習に関連する、一連のユーザー設定情報です)。読み込まれるリソースは、UI カルチャ設定によって決まります。 UI カルチャは、Web.config ファイルとページ ディレクティブの `UICulture` として設定され、Visual Basic または C# コードでは <xref:System.Globalization.CultureInfo.CurrentUICulture%2A> として設定されます。 カルチャ設定によって、日付、数値、通貨などの値の形式が決まります。 カルチャは、Web.config ファイルとページ ディレクティブでは `Culture` として設定され、Visual Basic または C# コードでは <xref:System.Globalization.CultureInfo.CurrentCulture%2A> として設定されます。

## <a name="see-also"></a>関連項目

- <xref:System.Globalization>
- <xref:System.Resources>
- [アプリケーションのグローバライズとローカライズ](../ide/globalizing-and-localizing-applications.md)
- [セキュリティおよびローカライズされたサテライト アセンブリ](../ide/security-and-localized-satellite-assemblies.md)