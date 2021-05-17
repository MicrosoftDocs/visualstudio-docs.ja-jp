---
title: 'テスト領域 8: プラグインの切り替え |Microsoft Docs'
description: このソース管理テスト領域には、Visual Studio のソリューションのソース管理に使用するプラグインを選択するプロセスのテスト ケースが用意されています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], switching plug-ins
- source control plug-ins, switching
ms.assetid: 01370792-b5da-4e46-9ce2-7dd326587141
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2dbc6b9646bcdec8cbdfae9d262397eb0ff74bdc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090773"
---
# <a name="test-area-8-plug-in-switching"></a>テスト領域 8: プラグインの切り替え
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) には、現在のソース管理プラグインを変更するためのユーザー インターフェイス (UI) が用意されています。 このテスト領域には、ソリューションのソース管理に使用するプラグインを選択するプロセスのテスト ケースが用意されています。

## <a name="command-menu-access"></a>コマンド メニューへのアクセス
 このテスト ケースでは、次の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境メニュー パスが使用されます。

- 現在のソース管理プラグイン: **[ツール]**  ->  **[オプション]**  ->  **[ソース管理]**  ->  **[プラグインの選択]** 。

- ソース管理のバインドの変更: **[ファイル]**  ->  **[ソース管理]**  ->  **[ソース管理の変更]** ...

## <a name="common-expected-behavior"></a>想定されている一般的な動作
 ソリューションのソース管理プラグインを変更するには、Visual Studio を終了したりソリューションを再読み込みしたりする必要はありません。 さらに、最新のソース管理プラグインは、ソリューションが読み込まれるときに、ソリューションによって使用されているものに自動的に変更されます。

## <a name="test-cases"></a>テスト ケース
 次に示すのは、プラグインの切り替えテスト領域の具体的なテスト ケースです。

### <a name="case-8a-automatic-change"></a>ケース 8a: 自動変更

#### <a name="expected-behavior"></a>想定されている動作
 ユーザーがソース管理下にあるソリューションを読み込むと、ソリューションが自動的に読み込まれ、適切なソース管理プラグインが最新のものとして選択されます。

| アクション | テスト ステップ | 確認が必要な期待される結果 |
| - | - | - |
| ソース管理プラグインの自動変更 | 1.  テスト中のプラグインを最新のものとして選択します ( **[ツール]**  ->  **[オプション]**  ->  **[ソース管理]**  ->  **[プラグインの選択]** )。<br />2.  新しいプロジェクトを作成します。<br />3.  ソース管理にソリューションを追加します。<br />4.  もう 1 つのプラグイン (たとえば、[!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)]) を選択します。<br />5.  ソリューションのアンロード プロンプトを受け入れます。<br />6.  ディスクからソリューションを再度開きます。 | ソリューションが開かれている。<br /><br /> テスト中のプラグインが、最新のソース管理プラグインである。 |

### <a name="case-8b-solution-based-change"></a>ケース 8b: ソリューションベースの変更

#### <a name="expected-behavior"></a>想定されている動作
 このソリューションでは、関連付けられたソース管理プラグインを変更することができます。

| アクション | テスト ステップ | 確認が必要な期待される結果 |
|----------------------------------| - | - |
| ソリューションのプラグインの変更 | 1.  テスト中のプラグインを最新のものとして選択します ( **[ツール]**  ->  **[オプション]**  ->  **[ソース管理]**  ->  **[プラグインの選択]** )。<br />2.  新しいプロジェクトとソリューションを作成します。<br />3.  ソース管理にソリューションを追加します。<br />4.  ソース管理からソリューションのバインドを解除します ( **[ソース管理の変更]** ダイアログ ボックスを使用します)。<br />5.  もう 1 つのプラグイン (たとえば、[!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)]) を選択します。<br />6.  アンロードされている場合は、ディスクからソリューションを再読み込みします。<br />7.  ソース管理にソリューションを追加します。<br />8.  ソース管理からソリューションのバインドを解除します ( **[ソース管理の変更]** ダイアログ ボックスを使用します)。<br />9. テスト中のプラグインをもう一度選択します。<br />10. アンロードされている場合は、ディスクからソリューションを再読み込みします。<br />11. ソリューションを元の場所にバインドします ( **[ソース管理の変更]** ダイアログ ボックスを使用します)。 | ソリューションが選択したプラグインを使用してソース管理に追加されている。 |

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン向けのテスト ガイド](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
