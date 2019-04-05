---
title: Windows インストーラーの配置の拡張機能の準備 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- vsix msi
ms.assetid: 5ee2d1ba-478a-4cb7-898f-c3b4b2ee834e
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2f37ed2819e1c5999c7d225e52f652ebef3bd7da
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56692113"
---
# <a name="prepare-extensions-for-windows-installer-deployment"></a>Windows インストーラーの配置の拡張機能を準備します。
Windows インストーラー パッケージ (MSI) を使用して、VSIX パッケージを配置することはできません。 ただし、MSI の展開用の VSIX パッケージの内容を抽出することができます。 このドキュメントでは、プロジェクトの既定の出力は、セットアップ プロジェクトに含めることの VSIX パッケージを準備する方法を示します。

## <a name="prepare-an-extension-project-for-windows-installer-deployment"></a>Windows インストーラーの配置の拡張機能プロジェクトを準備します。
 セットアップ プロジェクトに追加する前に、新しい拡張機能プロジェクトに次の手順を実行します。

### <a name="to-prepare-an-extension-project-for-windows-installer-deployment"></a>Windows インストーラーの配置の拡張機能プロジェクトを準備するには

1.  VSPackage、MEF コンポーネント、エディターの表示要素、または VSIX マニフェストを含むその他の機能拡張プロジェクトの種類を作成します。

2.  VSIX マニフェスト、コード エディターで開きます。

3.  設定、 `InstalledByMsi` VSIX マニフェストの要素`true`します。 VSIX マニフェストの詳細については、[VSIX 拡張機能スキーマ 2.0 リファレンス](../extensibility/vsix-extension-schema-2-0-reference.md)を参照してください。

     これは、VSIX インストーラーが、コンポーネントをインストールしようとすることを防ぎます。

4.  プロジェクトを右クリックして**ソリューション エクスプ ローラー**クリック**プロパティ**します。

5.  選択、 **VSIX**タブ。

6.  チェック ボックスをオン**次の場所にコピー VSIX コンテンツ**セットアップ プロジェクトは、ファイルを集荷するパスを入力します。

## <a name="extract-files-from-an-existing-vsix-package"></a>既存の VSIX パッケージからファイルを抽出します。
 ソース ファイルを持っていない場合は、セットアップ プロジェクトに既存の VSIX パッケージのコンテンツを追加する手順を実行します。

### <a name="to-extract-files-from-an-existing-vsix-package"></a>既存の VSIX パッケージからファイルを抽出するには

1.  名前の変更、*します。VSIX*ファイルから拡張機能を含む*filename.vsix*に*filename.zip*します。

2.  内容をコピー、 *.zip*ディレクトリにファイル。

3.  削除、 *[Content_types] .xml*ディレクトリからファイル。

4.  前の手順で示すように、VSIX マニフェストを編集します。

5.  セットアップ プロジェクトに、残りのファイルを追加します。

## <a name="see-also"></a>関連項目
- [Visual Studio インストーラーの配置](https://msdn.microsoft.com/library/121be21b-b916-43e2-8f10-8b080516d2a0)
- [チュートリアル: カスタム アクションを作成します。](/previous-versions/visualstudio/visual-studio-2010/d9k65z2d(v=vs.100))