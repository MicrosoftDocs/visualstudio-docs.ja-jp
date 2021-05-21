---
title: XAML のエラーと警告
description: エラーの分類方法、エラー情報の取得方法、およびそれらを修正するためのオプションの検索方法など、Visual Studio での XAML のエラーと警告について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/06/2018
ms.topic: error-reference
ms.assetid: 34eac8a0-7ec5-4c40-b97a-0126ed367931
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e33cdc11eb5531fd2325bd90912dc22a105711c5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99903647"
---
# <a name="xaml-errors-and-warnings"></a>XAML のエラーと警告

Visual Studio では、XAML を作成するとき、入力したコードがすぐに解析されます。 エラーが検出されると、コード行に波線が付きます。 この波線にマウス カーソルを合わせると、エラーまたは警告に関する詳細が表示されます。 一部のエラーと警告にはクイック アクションの電球が表示されます。**Ctrl**+ **.** キーボード ショートカットで 問題解決のための選択肢が表示されます。

## <a name="error-types"></a>エラーの種類

バックグラウンドでは、複数のツールにより並列で XAML が解析されます。 XAML エラーは、エラーを検出したツールに基づき、次の 3 つの種類の 1 つに分類されます。

|**エラーを検出した機能**|**エラー コードの形式**|**Visual Studio のバージョン**|
| - |-----------------| - |
|XAML 言語サービス (XAML エディター)|XLSxxxx| すべてのバージョン |
|XAML デザイナー|XDGxxxx| すべてのバージョン | 
|XAML のエディット コンティニュ|XECxxxx| Visual Studio 2019 バージョン 16.1 以前 |
|XAML ホット リロード | XHRxxxx | Visual Studio 2019 バージョン 16.2 以降 |

XAML のエディット コンティニュから XAML ホット リロードへのブランド変更の詳細については、[リリース ノート](/visualstudio/releases/2019/release-notes-v16.2#wpfuwp-tooling)を参照してください

> [!Note]
> 一部のエラーや警告には該当コードがありません。 そのようなエラーは通常、XAML デザイナーが検出したエラーです。

## <a name="suppress-xaml-designer-errors"></a>XAML デザイナー エラー

**[ツール]、[オプション]** の順に選択して **[オプション]** ダイアログを開き、**[テキスト エディター]、[XAML]、[その他]** の順に選択します。

**[Show errors detected by the XAML designer]\(XAML デザイナーによって検出されたエラーを表示する\)** チェック ボックスの選択を解除します。

![XAML デザイナー エラー](media/suppress_xaml_designer_errors.png)