---
title: '方法: スクリプトドキュメントを表示する |Microsoft Docs'
ms.date: 11/05/2019
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Script Explorer
ms.assetid: 8b621e53-4508-4b4a-9995-70995b0b9ac8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5e362e0504c4ed2584bbbbea687fe3c58fc79edb
ms.sourcegitcommit: ba0fef4f5dca576104db9a5b702670a54a0fcced
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73714438"
---
# <a name="how-to-view-script-documents-javascript"></a>方法: スクリプトドキュメントを表示する (JavaScript)

サーバー側のスクリプトファイルはソリューションエクスプローラーに表示されます。 クライアント側スクリプト ファイルは、デバッグ モードまたは中断モードのときにのみ表示されます。 クライアント側のスクリプトファイルは、**スクリプトドキュメント**ノードに表示されます。

ページを動的に生成するアプリケーションの種類によっては、ブラウザーに読み込まれたスクリプトドキュメントからブレークポイントを設定すると、中断モードとデバッグが簡単になります。 同様に、読み込まれたスクリプトドキュメントから `debugger` ステートメントを追加して、中断モードにすることができます。 この記事では、これらのドキュメントを表示する方法について説明します。

> [!NOTE]
> [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)]以前は、サーバー側スクリプトから生成されたクライアント側スクリプトファイルは [スクリプトエクスプローラー] ウィンドウに表示されていました。

### <a name="to-view-a-server-side-script-document"></a>サーバー側スクリプト ドキュメントを表示するには

1. **ソリューション エクスプローラー**で、 **[\<Website Pathname>]** ノードを開きます。

2. 表示するスクリプト ファイルをダブルクリックします。

     サーバー側スクリプト ファイルがソース ウィンドウに表示されます。

### <a name="to-view-a-client-side-script-document"></a>クライアント側スクリプト ドキュメントを表示するには

1. **ソリューション エクスプローラー**で、 **[スクリプト ドキュメント]** ノードを開きます。

2. 表示するスクリプト ファイルをダブルクリックします。

     クライアント側スクリプト ファイルがソース ウィンドウに表示されます。

## <a name="see-also"></a>関連項目
- [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)