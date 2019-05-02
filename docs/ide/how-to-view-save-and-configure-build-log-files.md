---
title: '方法: ビルド ログ ファイルを表示、保存、および構成する | Microsoft Docs'
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: conceptual
ms.assetid: 75d38b76-26d6-4f43-bbe7-cbacd7cc81e7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e40f414b3b3ea6bc151ef036deb0b5d80464ba46
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62429146"
---
# <a name="how-to-view-save-and-configure-build-log-files"></a>方法: ビルド ログ ファイルを表示、保存、および構成する

Visual Studio IDE でプロジェクトをビルドしたら、**[出力]** ウィンドウでそのビルドに関する情報を表示できます。 この情報を使用して、たとえば、ビルド エラーをトラブルシューティングできます。 

- C++ のプロジェクトでは、自動的に作成および保存された *.txt* ファイルで同じ情報を確認することもできます。 

- マネージド コード プロジェクトでは、ビルド出力ウィンドウ内をクリックし、**Ctrl**+**S** キーを押します。 Visual Studio から、**[出力]** ウィンドウの情報を保存する *.txt* ファイルの場所を指定することを求められます。 

また、IDE を使用すれば、各ビルドについて、表示する情報の種類を指定することもできます。

MSBuild を使用して任意の種類のプロジェクトをビルドする場合は、ビルドに関する情報を保存する *.txt* ファイルを作成することができます。 詳細については、[ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)に関するページを参照してください。

## <a name="to-view-the-build-log-file-for-a-c-project"></a>C++ プロジェクトのビルド ログ ファイルを表示するには

1. **Windows エクスプローラー**または**エクスプローラー**で、次のファイルを開きます。*\\...\Visual Studio \<バージョン\>\Projects\\<プロジェクト名\>\\<プロジェクト名\>\Debug\\<プロジェクト名\>.txt*

## <a name="to-create-a-build-log-file-for-a-managed-code-project"></a>マネージ コード プロジェクトのビルド ログ ファイルを作成するには

1. メニュー バーで、**[ビルド]** > **[ソリューションのビルド]** の順にクリックします。

2. **[出力]** ウィンドウで、テキスト内のどこかをクリックします。

3. **Ctrl**+**S** を押します。

   Visual Studio から、ビルド出力を保存する場所を指定することを求められます。

## <a name="to-change-the-amount-of-information-included-in-the-build-log"></a>ビルド ログに含める情報の量を変更するには

1. メニュー バーの **[ツール]**  >  **[オプション]** の順にクリックします。

2. **[プロジェクトおよびソリューション]** ページで、**[ビルド/実行]** ページを選択します。

3. **[MSBuild プロジェクト ビルドの出力の詳細]** の一覧で、次の値のいずれかを選択し、**[OK]** ボタンを選択します。

    |詳細レベル|説明|
    | - |-----------------|
    |**非表示**|ビルドの概要のみを表示します。|
    |**最小限**|ビルドの概要と、重要度 - 高として分類されたエラー、警告、メッセージを表示します。|
    |**標準**|ビルドの概要と、重要度 - 高として分類されたエラー、警告、およびメッセージと、ビルドの主なステップとを表示します。 この詳細レベルを最も頻繁に使用します。|
    |**詳細**|ビルドの概要と、重要度 - 高として分類されたエラー、警告、およびメッセージと、ビルドのすべてのステップと、標準的な重要度として分類されたメッセージとを表示します。|
    |**診断**|ビルドで使用できるすべてのデータを表示します。 このレベルの詳細は、カスタム ビルド スクリプトの問題およびその他のビルドの問題をデバッグする場合に役に立ちます。|

     詳細については、「[[オプション] ダイアログ ボックス、[プロジェクトおよびソリューション]、[ビルド/実行]](../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md)」および「<xref:Microsoft.Build.Framework.LoggerVerbosity>」を参照してください。

    > [!IMPORTANT]
    > **[出力]** ウィンドウ (すべてのプロジェクト) と *\<ProjectName>.txt* ファイル (C++ プロジェクトのみ) に変更を反映するには、プロジェクトをリビルドする必要があります。

## <a name="see-also"></a>関連項目

- [ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)
- [Visual Studio でのプロジェクトとソリューションのビルドおよびクリーン](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
- [コンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
