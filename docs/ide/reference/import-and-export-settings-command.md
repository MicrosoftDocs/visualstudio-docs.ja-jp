---
description: Visual Studio の設定をインポート、エクスポート、またはリセットします。 vssettings ファイル拡張子
title: '[設定のインポートとエクスポート] コマンド'
ms.date: 05/28/2021
ms.topic: reference
f1_keywords:
- Tools.ImportandExportSettings
helpviewer_keywords:
- Tools.ImportandExportSettings
- Import and Export Settings command
ms.assetid: 94a06468-a44d-403d-a931-77bbc9d06e56
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: dba50cf598c3c74f6c9407fbef5d55f938941a11
ms.sourcegitcommit: 63cb90e8cea112aa2ce8741101b309dbc709e393
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2021
ms.locfileid: "110687641"
---
# <a name="import-and-export-settings-command-vssettings-file"></a>[設定のインポートとエクスポート] コマンド (.vssettings ファイル)

Visual Studio の設定ファイル `.vssettings` をインポート、エクスポート、またはリセットします。

ファイルのスキーマが開いています。 最も一般的には、スキーマは XML 構造に従います。その構造では、各カテゴリはタグであり、それ自体にサブカテゴリ タグを含めることができます。 これらのサブカテゴリ タグには、プロパティ値タグを含めることができます。 ほとんどのパッケージでは共通の構造を使用されますが、Visual Studio 内のパッケージはすべて、選択したスキーマを使用して任意の XML をファイルに提供できます。

## <a name="syntax"></a>構文

```cmd
Tools.ImportandExportSettings [/export:filename | /import:filename | /reset]
```

## <a name="switches"></a>スイッチ

/export:`filename`

省略可能。 現在の設定を指定したファイルにエクスポートします。

/import:`filename`

省略可能。 設定を指定したファイルからインポートします。

/reset

省略可能。 現在の設定をリセットします。

## <a name="remarks"></a>解説

スイッチを指定しないでこのコマンドを実行すると、**[設定のインポートとエクスポート]** ウィザードが開きます。 詳細については、[設定の同期](../synchronized-settings-in-visual-studio.md)と[環境設定](../environment-settings.md)に関するページを参照してください。

## <a name="example"></a>例

次のコマンドは、現在の設定を `MyFile.vssettings` ファイルにエクスポートします。

```cmd
Tools.ImportandExportSettings /export:"c:\Files\MyFile.vssettings"
```



## <a name="see-also"></a>関連項目

- [環境設定](../../ide/environment-settings.md)
- [設定を同期する](../../ide/synchronized-settings-in-visual-studio.md)
- [Visual Studio IDE のカスタマイズ](../../ide/personalizing-the-visual-studio-ide.md)
- [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)
