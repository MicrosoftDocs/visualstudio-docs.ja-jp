---
title: ローカルのヘルプ ドキュメントのインストール
description: Microsoft ヘルプ ビューアーを使用し、ローカルのヘルプ ドキュメントをインストールし、管理します。 コンピューターにインストールされるヘルプ コンテンツの追加、削除、更新、移動を行います。
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- hv_manage
helpviewer_keywords:
- changing content installation source [Help Viewer]
- updating local content [Help Viewer]
- Help Viewer, content installation source
- Help Viewer, updating local content
- Help Viewer, changing content installation source
- installing local content [Help Viewer]
- content installation source [Help Viewer]
- downloading content [Help Viewer]
- removing local content [Help Viewer]
- Help Viewer, removing local content
- Help Viewer, installing local content
- Help Viewer, downloading content
ms.assetid: efd9df4c-2e69-4c50-992c-9678a8d8cf19
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 14091ecd5adc76762901c02c582c845aa0dbd513
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99944122"
---
# <a name="install-and-manage-local-content"></a>ローカル コンテンツのインストールと管理

Microsoft ヘルプ ビューアーを使用すると、ソフトウェア開発のニーズに合わせてコンピューターにインストールされているヘルプ コンテンツを追加、削除、更新、移動できます。

ローカル コンピューターのコンテンツを管理するには、管理者アクセス許可を持つアカウントでログオンする必要があります。 また、システム管理者が組織のローカル コンテンツ管理の意志決定を行うため、エンタープライズ環境で作業している場合、ローカル コンテンツを管理できない場合があります。 詳細については、「[ヘルプ ビューアーの管理者ガイド](../help-viewer/administrator-guide.md)」を参照してください。

## <a name="change-the-content-installation-source"></a>コンテンツのインストール元を変更する

既定では、ヘルプ ビューアーはソースとして Microsoft のオンライン サービスを使用してコンテンツをインストールします。 システム管理者が別の場所にコンテンツを既にインストールしているエンタープライズ環境で作業している場合を除き、一般にコンテンツ ソースを変更しないでください。

### <a name="to-change-the-content-installation-source"></a>コンテンツのインストール元を変更するには

1. **[コンテンツの管理]** タブで、**[ディスク]** オプション ボタンを選択します。

    > [!NOTE]
    > **[ディスク]** オプションは、管理者がコンテンツのインストール元を変更できないように設定している場合、使用できません。 詳細については、「[ヘルプ ビューアーの管理者ガイド](../help-viewer/administrator-guide.md)」を参照してください。

2. 次のいずれかの操作を実行します。

    - *.msha* ファイルのパスまたはサービス エンドポイントの URL を入力します。

    - 参照 **[…]** ボタンを選択して *.msha* ファイルに移動します。

    - 一覧で、最後に使用されたエントリを選択します。

## <a name="download-and-install-content-locally"></a>ローカルへのコンテンツのダウンロードおよびインストール

ローカル コンピューターにコンテンツをダウンロードしてインストールすると、インターネット接続なしでトピックを表示できます。

> [!IMPORTANT]
> コンテンツをインストールするには、管理権限を持つアカウントでログオンする必要があります。

> [!NOTE]
> Visual Studio IDE が英語以外の言語に設定されている場合、英語のコンテンツまたはローカライズされたコンテンツ、あるいはその両方をインストールできます。 ただし、英語バージョンのみをインストールしていて、**[ビューアーのオプション]** ダイアログ ボックスの **[すべてのナビゲーション タブおよび F1 要求に英語版コンテンツを含める]** チェック ボックスがオフになっている場合、コンテンツは表示されません。

### <a name="to-download-and-install-content"></a>コンテンツをダウンロードおよびインストールするには

1. **[コンテンツの管理]** タブを選択します。

2. コンテンツの一覧で、ダウンロードしてインストールするブックの隣にある **[追加]** リンクを選択します。

     ブックが **[保留中の変更]** の一覧に追加され、指定したブックの予想サイズがその一覧の下に表示されます。 一部のブックはトピックを共有しているため、複数のブックの合計ダウンロード サイズは、指定したすべてのブックのサイズを加算した結果よりも小さい場合があります。

3. **[更新]** ボタンを選択します。

     指定したブックは、コンピューターに既にあるブックの更新と共にインストールされます。 インストール時間は変化しますが、ステータス バーで進行状況を確認できます。

## <a name="remove-local-content"></a>ローカル コンテンツを削除する

コンピューターから不要なコンテンツを削除することにより、ディスク領域を節約できます。

> [!IMPORTANT]
> コンテンツを削除するには、管理者権限が必要です。

> [!NOTE]
> Visual Studio IDE が英語以外の言語に設定されており、ローカライズされたコンテンツを削除し、**[ビューアー オプション]** ダイアログ ボックスの **[すべてのナビゲーション タブおよび F1 要求に英語版コンテンツを含める]** チェック ボックスをオフにした場合、コンテンツは表示されません。

### <a name="to-remove-content"></a>コンテンツを削除するには

1. **[コンテンツの管理]** タブを選択します。

2. コンテンツの一覧で、削除するブックの隣にある **[削除]** リンクを選択します。

     ブックが **[保留中の変更]** 一覧に追加されます。

3. **[更新]** ボタンを選択します。

     指定したブックがコンピューターから削除されます。

## <a name="update-local-content"></a>ローカル コンテンツを更新する

ステータス バーは、インストールされたコンテンツへの更新が使用可能なことが示されます。

> [!IMPORTANT]
> **ヘルプ ビューアー** で自動的にオンライン更新を確認する場合、**[ビューアーのオプション]** ダイアログ ボックスを開き、**[オンラインでコンテンツを取得し、コンテンツの更新をチェックする]** チェック ボックスをオンにする必要があります。

### <a name="to-update-local-content"></a>ローカル コンテンツを更新するには

- ステータス バーの右下隅の **[今すぐダウンロードするにはここをクリックします]** リンクを選択します。

更新時間は変化する可能性がありますが、ステータス バーで更新の進行状況を確認できます。

## <a name="move-local-content"></a>ローカル コンテンツを移動する

ローカル コンピューターから、ローカル コンピューター上のネットワーク共有または別のパーティションに、インストールされたコンテンツを移動することによって、ディスク領域を節約できます。

> [!IMPORTANT]
> コンテンツを移動するには、管理権限を持つアカウントでログオンする必要があります。

### <a name="to-move-local-content"></a>ローカル コンテンツを移動するには

1. **[コンテンツの管理]** タブで、**[ローカル ストア パス]** の下にある **[移動]** ボタンを選択します。

     **[コンテンツの移動]** ダイアログ ボックスが開きます。

2. **[移動先]** ボックスにコンテンツの別の場所を入力し、**[OK]** をクリックします。

3. コンテンツが移動したら、**[閉じる]** をクリックします。

## <a name="see-also"></a>関連項目

- [Microsoft ヘルプ ビューアー](../help-viewer/overview.md)