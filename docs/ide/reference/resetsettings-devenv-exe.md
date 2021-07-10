---
title: -ResetSettings (devenv.exe)
description: devenv の ResetSettings コマンドライン スイッチを使用して、Visual Studio の既定の設定を復元し、Visual Studio IDE を自動的に起動する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- Devenv, /ResetSettings switch
- ResetSettings switch
- /ResetSettings Devenv switch
- settings [Visual Studio], resetting
ms.assetid: 1d41021c-6f58-4bd5-b122-d1c995812192
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e523738ff23b40c80b5df21d90b582d94c59087f
ms.sourcegitcommit: a8031c1387d2090129ed33e063744f9f31653dcd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2021
ms.locfileid: "110724539"
---
# <a name="resetsettings-devenvexe"></a>/ResetSettings (devenv.exe)

Visual Studio の既定の設定を復元し、Visual Studio IDE を自動的に起動します。 このスイッチで、指定した設定ファイル (`*.vssettings`) に準じた設定にリセットすることもできます。

既定の設定は、Visual Studio の初回起動時に選択したプロファイルから取得されます。

> [!TIP]
> 統合開発環境 (IDE) を使用して設定をリセットする方法については、「[リセット設定](../environment-settings.md#reset-settings)」を参照してください。

## <a name="syntax"></a>構文

```shell
devenv /ResetSettings [SettingsFile|DefaultCollectionSpecifier]
```

## <a name="arguments"></a>引数

- *SettingsFile*

  任意。 Visual Studio に適用する `.vssettings` ファイルの完全なパスとファイル名。

- *DefaultCollectionSpecifier*

  任意。 復元する設定の既定のコレクションを表す指定子。 この表に記載されている既定のコレクション指定子のいずれかを選択してください。

  | 既定のコレクション名 | コレクション指定子 |
  | --- | --- |
  | **全般** | `General` |
  | **JavaScript** | `JavaScript` |
  | **Visual Basic** | `VB` |
  | **Visual C#** | `CSharp` |
  | **Visual C++** | `VC` |
  | **Web 開発** | `Web` |
  | **Web 開発 (コードのみ)** | `WebCode` |

## <a name="remarks"></a>注釈

*SettingsFile* が指定されていない場合、既存の設定を使用して IDE が開きます。 


## <a name="example"></a>例

最初の例では、`MySettings.vssettings` ファイルに保存された設定を適用します。

2 つ目の例では、Visual C# の既定のプロファイルを復元します。

3 つ目の例ではまた、設定の適用後に Visual Studio が閉じられます。 `/Command "File.Exit"` を追加できます。

```shell
devenv /ResetSettings "%USERPROFILE%\MySettings.vssettings"

devenv /ResetSettings CSharp

devenv /NoSplash /ResetSettings General /Command Exit 
```

## <a name="see-also"></a>関連項目

- [環境設定](../environment-settings.md)
- [Visual Studio IDE のカスタマイズ](../../ide/personalizing-the-visual-studio-ide.md)
- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
