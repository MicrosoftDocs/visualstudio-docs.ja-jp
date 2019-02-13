---
title: コード化された UI テストと操作の記録を拡張する
ms.date: 11/04/2016
ms.topic: conceptual
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 07cdc27cb47a6de46585f573d78b5af00631c2a2
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55951190"
---
# <a name="extend-coded-ui-tests-and-action-recordings"></a>コード化された UI テストと操作の記録を拡張する

コード化された UI テストおよび操作の記録のテスト フレームワークは、すべてのユーザー インターフェイスでサポートされているとは限りません。 テストする特定の UI がサポートされていない場合があります。 たとえば、Microsoft Excel スプレッドシート向けのコード化された UI テストや操作の記録をすぐに作成することはできません。 ただし、コード化された UI テスト フレームワークの拡張機能を使用すると、特定の UI をサポートするコード化された UI テスト フレームワーク向けの独自の拡張機能を作成できます。

![UI テストのアーキテクチャ](../test/media/ui_testarch.png)

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="sample-extension-to-test-microsoft-excel"></a>Microsoft Excel をテストするサンプル拡張機能

この[ブログ記事](https://blogs.msdn.microsoft.com/gautamg/2010/01/05/3-introducing-sample-excel-extension/)には、コード化された UI テスト フレームワーク用の[サンプル拡張機能](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Components.PostAttachments/00/09/94/38/24/ExcelPluginSample.zip)へのリンクが含まれています。 また、[コード化された UI テストの拡張性に関するブログ記事シリーズ](https://blogs.msdn.microsoft.com/gautamg/2010/01/05/series-on-coded-ui-test-extensibility/)全体を表示することもできます。

> [!NOTE]
> サンプルは、Microsoft Excel 2010 での使用を意図しています。 その他のバージョンの Excel では、動作する場合と動作しない場合があります。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider>
- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement>
- <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UITestActionFilter>
- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage>
- [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)
- [コード化された UI テストのベスト プラクティス](../test/best-practices-for-coded-ui-tests.md)
- [コード化された UI テストと操作の記録でサポートされている構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)