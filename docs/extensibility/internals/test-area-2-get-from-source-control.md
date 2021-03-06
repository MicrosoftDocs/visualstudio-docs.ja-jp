---
title: 'テスト領域 2: ソース管理からの取得 | Microsoft Docs'
description: このテスト領域は、Get を使用してバージョン ストアから項目を取得するためのテスト ケースに対応します。 これらのテスト ケースは、ローカル プロジェクトと Web プロジェクトの両方に適用できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting items from source control
- source control [Visual Studio SDK], getting items from
ms.assetid: cbd345c5-ca43-4630-b7a4-85564f4e2090
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ab6a35aa896d7a68e151007d6f694672f7477688
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073431"
---
# <a name="test-area-2-get-from-source-control"></a>テスト領域 2: ソース管理から取得
このテスト領域は、Get コマンド経由でバージョン ストアから項目を取得するためのテスト ケースに対応します。 これらのテスト ケースは、ローカル プロジェクトと Web プロジェクトの両方に適用できます。

## <a name="command-menu-access"></a>コマンド メニューへのアクセス
 このテスト ケースでは、次の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境メニュー パスが使用されます。

##### <a name="get-latest-version"></a>最新バージョンの取得:

- **[ファイル]** 、 **[ソース管理]** 、 **[最新バージョンを取得する]** 。

- **[ファイル]** 、 **[最新バージョンを取得する]** 。

- ショートカット メニュー、 **[最新バージョンを取得する]** 。

- Get: **[ファイル]** 、 **[ソース管理]** 、 **[取得]** 。

## <a name="expected-behavior"></a>想定されている動作

##### <a name="get-latest-version"></a>最新バージョンの取得:
 バージョン ストアからの最新バージョンの項目の自動的な (UI なし) 取得を実行します。

##### <a name="get"></a>Get: 
 **[取得]** ダイアログ ボックスが表示され、ユーザーは、取得されるファイル セットに変更を加え、ファイルの取得方法に影響するオプションを変更することができます。

## <a name="test-cases"></a>テスト ケース

|アクション|テスト ステップ|確認が必要な期待される結果|
|------------|----------------|--------------------------------|
|ローカルに存在しないファイルの最新バージョンを取得する|1. プロジェクトを作成します。<br />2. プロジェクトにアイテムを追加します。<br />3. プロジェクトをソース管理下に置きます。<br />4. 項目のローカル コピーを削除します。<br />5. 項目の最新バージョンを取得します (ショートカット メニュー、 **[最新バージョンを取得する]** )。|項目ファイルがローカルに取得されます。|
|ローカルに存在しないファイルを取得する|1. プロジェクトを作成します。<br />2. プロジェクトにアイテムを追加します。<br />3. プロジェクトをソース管理下に置きます。<br />4. 項目のローカル コピーを削除します。<br />5. 項目を取得します ( **[ファイル]** 、 **[ソース管理]** 、 **[** の取得]\<item>)。|項目ファイルがローカルに取得されます。|
|排他的にチェックアウトされ、ローカルで変更されたファイルを取得する|1. プロジェクトを作成します。<br />2. プロジェクトにアイテムを追加します。<br />3. プロジェクトをソース管理下に置きます。<br />4. プロジェクト項目を排他的にチェックアウトします。<br />5. ローカル コピーを変更します。<br />6. 項目の最新バージョンを取得します ( **[ファイル]** 、 **[** の最新バージョンを取得する]\<item>)。 この手順が成功した場合は、次の手順に進みます。<br />7. 警告ダイアログ ボックスの **[置換]** ボタンをクリックします。|**手順 6 の結果** `:`<br /><br /> 警告ダイアログ ボックスに、ファイルがチェックアウトされていることが示されます。<br /><br /> **手順 7 の結果:**<br /><br /> 変更されたローカル ファイルは、バージョン ストアの元のバージョンによって置き換えられます。<br /><br /> ファイルは読み取り/書き込みです。|
|ローカルにチェックアウトされ、共有、および変更されたファイルを取得して置換する|1. 新しいプロジェクトを作成します。<br />2. プロジェクトにアイテムを追加します。<br />3. プロジェクトをソース管理下に置きます。<br />4. プロジェクト項目を共有としてチェックアウトします。<br />5. ローカル コピーを変更します。<br />6. 項目の最新バージョンを取得します ( **[ファイル]** 、 **[** の最新バージョンを取得する]\<item>)。 この手順が成功した場合は、次の手順に進みます。<br />7. 警告ダイアログ ボックスの **[置換]** をクリックします。|**手順 6 の結果:**<br /><br /> 警告ダイアログ ボックスに、ファイルがチェックアウトされていることが示されます。<br /><br /> **手順 7 の結果:**<br /><br /> 変更されたローカル ファイルは、バージョン ストアの元のバージョンによって置き換えられます。<br /><br /> ファイルは読み取り/書き込みです。|
|ローカルに存在する、バージョン ストアの最新バージョンと同じファイルを取得する|1. 新しいプロジェクトを作成します。<br />2. プロジェクトにアイテムを追加します。<br />3. プロジェクトをソース管理下に置きます。<br />4. 項目を取得します ( **[ファイル]** 、 **[ソース管理]** 、 **[** の取得]\<item>)。|ローカル ファイルは変更されていません。|
|1 つのプロジェクトを含むソリューションを取得する|1. 1 つのプロジェクトを含むソリューションを作成します。<br />2. ソリューションをソース管理下に置きます。<br />3. すべてのプロジェクト ファイルをローカルで削除します。<br />4. ソリューションを取得します ( **[ファイル]** 、 **[ソース管理]** 、 **[取得]** )。|削除されたファイルはすべてローカルに復元されます。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン向けのテスト ガイド](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
