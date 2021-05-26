---
title: Windows インストーラーのデプロイに関する拡張機能を準備する | Microsoft Docs
description: 既定の出力がセットアップ プロジェクトに含める VSIX パッケージであるプロジェクトを準備する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- vsix msi
ms.assetid: 5ee2d1ba-478a-4cb7-898f-c3b4b2ee834e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6436d05d3b15be1c1fe8d7c7bb9c8592dee091dc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090279"
---
# <a name="prepare-extensions-for-windows-installer-deployment"></a>Windows インストーラーのデプロイに関する拡張機能を準備する
Windows インストーラー パッケージ (MSI) を使用して VSIX パッケージをデプロイすることはできません。 ただし、MSI のデプロイ用に VSIX パッケージのコンテンツを抽出することはできます。 このドキュメントでは、既定の出力がセットアップ プロジェクトに含める VSIX パッケージであるプロジェクトを準備する方法について説明します。

## <a name="prepare-an-extension-project-for-windows-installer-deployment"></a>Windows インストーラーのデプロイ用の拡張機能プロジェクトを準備する
 セットアップ プロジェクトに追加する前に、新しい拡張機能プロジェクトでこれらの手順を実行します。

### <a name="to-prepare-an-extension-project-for-windows-installer-deployment"></a>Windows インストーラーのデプロイ用の拡張機能プロジェクトを準備するには

1. VSPackage、MEF コンポーネント、エディターの表示要素、または VSIX マニフェストを含むその他の拡張性プロジェクト タイプを作成します。

2. コード エディターで VSIX マニフェストを開きます。

3. VSIX マニフェストの `InstalledByMsi` 要素を `true` に設定します。 VSIX マニフェストの詳細については、「[VSIX 拡張機能スキーマ 2.0 リファレンス](../extensibility/vsix-extension-schema-2-0-reference.md)」を参照してください。

     これで、VSIX インストーラーではコンポーネントのインストールを試行しなくなります。

4. **ソリューション エクスプローラー** でプロジェクトを右クリックし、 **[プロパティ]** をクリックします。

5. **[VSIX]** タブを選択します。

6. **[VSIX のコンテンツを次の場所にコピーする]** というラベルの付いたボックスをオンにし、セットアップ プロジェクトでファイルを取得するパスを入力します。

## <a name="extract-files-from-an-existing-vsix-package"></a>既存の VSIX パッケージからファイルを抽出する
 ソース ファイルがない場合に既存の VSIX パッケージのコンテンツをセットアップ プロジェクトに追加するには、次の手順を実行します。

### <a name="to-extract-files-from-an-existing-vsix-package"></a>既存の VSIX パッケージからファイルを抽出するには

1. 拡張機能を含む *.VSIX* ファイルの名前を *filename.vsix* から *filename.zip* に変更します。

2. *.zip* ファイルのコンテンツをディレクトリにコピーします。

3. ディレクトリから *[Content_types].xml* ファイルを削除します。

4. 前の手順で示したように、VSIX マニフェストを編集します。

5. 残りのファイルをセットアップ プロジェクトに追加します。

## <a name="see-also"></a>関連項目
- [Visual Studio インストーラーのデプロイ](/previous-versions/2kt85ked(v=vs.120))
- [チュートリアル: カスタム アクションの作成](/previous-versions/visualstudio/visual-studio-2010/d9k65z2d(v=vs.100))