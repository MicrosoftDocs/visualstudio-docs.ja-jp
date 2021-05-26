---
title: 'チュートリアル: Visual Studio の拡張機能を公開する |Microsoft Docs'
description: Visual Studio の拡張機能を Visual Studio Marketplace に公開する方法について説明します。こうすることで、開発者は新しい拡張機能と更新された拡張機能を参照できます。
ms.custom: SEO-VS-2020
ms.date: 01/15/2021
ms.topic: how-to
helpviewer_keywords:
- publishing web controls
- web controls, publishing
ms.assetid: a7816161-0490-4043-86f5-0f7331ed83b3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5b1ff7d55f7d667ca8b07134e144ad192b9d19d8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078358"
---
# <a name="walkthrough-publish-a-visual-studio-extension"></a>チュートリアル: Visual Studio の拡張機能を公開する

このチュートリアルでは、Visual Studio の拡張機能を Visual Studio Marketplace に公開する方法について説明します。 拡張機能を Visual Studio Marketplace に追加すると、開発者は **[拡張機能と更新プログラム]** を使用して、新しい拡張機能と更新された拡張機能を参照できます。

## <a name="prerequisites"></a>必須コンポーネント

 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-visual-studio-extension"></a>Visual Studio の拡張機能を作成する

この記事では、既定の VSPackage 拡張機能を使用していますが、すべての種類の拡張機能において同じ手順を実行できます。

- メニュー コマンドを含む `TestPublish` という名前の VSPackage を C# で作成します。 詳細については、[拡張機能 (Hello World) の初めての作成](../extensibility/extensibility-hello-world.md)に関するページを参照してください。

## <a name="package-your-extension"></a>拡張機能をパッケージ化する

1. 製品名、作成者、およびバージョンに関する正しい情報を使用して、拡張機能 *vsixmanifest* を更新します。

   ![拡張機能 vsixmanifest を更新する](media/update-extension-vsixmanifest.png)

2. 拡張機能を **リリース** モードでビルドします。 これで、拡張機能は \bin\Release フォルダーに VSIX としてパッケージ化されます。

3. VSIX をダブルクリックして、インストールを確認できます。

## <a name="test-the-extension"></a>拡張機能をテストする

 拡張機能を配布する前に、それをビルドしてテストし、Visual Studio の実験用インスタンスに正しくインストールされていることを確認します。

1. Visual Studio で、デバッグを開始して、Visual Studio の実験用インスタンスを開きます。

2. 実験用インスタンスで、 **[ツール]** メニューに移動して、 **[拡張機能と更新プログラム]** をクリックします。 TestPublish 拡張機能が中央のウィンドウに表示され、有効になります。

3. **[ツール]** メニューに、[テスト] コマンドが表示されていることを確認します。

## <a name="publish-the-extension-to-visual-studio-marketplace"></a>拡張機能を Visual Studio Marketplace に公開する

1. リリース バージョンの拡張機能がビルドされていること、およびそれが最新の状態であることを確認します。

2. Web ブラウザーで [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) にアクセスします。

3. 右上隅の **[サインイン]** をクリックします。

4. Microsoft アカウントを使用してサインインします。 Microsoft アカウントがない場合は、ここで新しく作成できます。

5. **[拡張機能の公開]** をクリックします。 このオプションを選択すると、すべての拡張機能の管理ページに移動します。 公開元のアカウントを持っていない場合は、この時点で作成するように求められます。

   ![Marketplace にアップロードする](media/upload-to-marketplace.png)

6. 拡張機能のアップロードに使用する公開元を選択します。 公開元を変更するには、左側に一覧表示されている公開元の名前をクリックします。 **[新しい拡張機能]** をクリックし、 **[Visual Studio]** を選択します。

7. **[1: 拡張機能をアップロード]** では、VSIX ファイルを Visual Studio Marketplace に直接アップロードするか、自身の Web サイトへのリンクを追加するのみにするかを選択できます。 この例では、拡張機能 *TestPublish.vsix* がアップロードされます。 拡張機能をドラッグ アンド ドロップするか、**クリック** リンクを使用してファイルを参照します。 プロジェクトの \bin\Release フォルダーで拡張機能を見つけます。  **[Continue]** をクリックします。

8. **[2: 拡張機能の詳細を指定]** の一部のフィールドには、拡張機能の *source.extension.vsixmanifest* ファイルから自動的に入力されます。 それぞれの詳細については、以下を参照してください。

    * **[内部名]** 。拡張機能の詳細ページの URL で使用されます。 たとえば、公開元名 "myname" で拡張機能を公開し、"my extension" という内部名を指定すると、拡張機能の詳細ページの URL が "marketplace.visualstudio\.com/items?itemName=myname.myextension" になります。

    * **[表示名]** 。拡張機能の表示名です。 この名前は、*source.extension.vsixmanifest* ファイルから自動的に入力されます。

    * **[バージョン番号]** 。アップロードする拡張機能のバージョン番号です。 このバージョンは、*source.extension.vsixmanifest* ファイルから自動的に入力されます。

    * **[VSIX ID]** 。Visual Studio で拡張機能に使用される一意識別子です。 拡張機能が自動更新されるようにする場合、この識別子が必要です。 この識別子は、*source.extension.vsixmanifest* ファイルから自動的に入力されます。

    * **[ロゴ]** 。拡張機能に使用されます。 このロゴは、*source.extension.vsixmanifest* ファイルから自動的に入力されます (指定されている場合)。

    * **[簡単な説明]** 。拡張機能の動作に関する簡単な説明です。 この説明は、*source.extension.vsixmanifest* ファイルから自動的に入力されます。

    * **[概要]** 。拡張機能の動作のスクリーンショットおよび詳細な情報を入力します。

    * **[サポートされている Visual Studio のバージョン]** 。拡張機能が動作する Visual Studio のバージョンを選択できます。 拡張機能は、これらのバージョンにのみインストールされます。

    * **[サポートされている Visual Studio のエディション]** 。拡張機能が動作する Visual Studio のエディションを選択できます。 拡張機能は、これらのエディションにのみインストールされます。

    * **[種類]** 。 最も一般的な拡張機能の種類は **ツール** です。

    * **[カテゴリ]** 。 拡張機能に最適なものを 3 つまで選択できます。

    * **[タグ]** 。ユーザーが拡張機能を検索するのに役立つキーワードです。 タグを使用すると、Visual Studio Marketplace で拡張機能が見つかる可能性が高くなります。

    * **[価格カテゴリ]** 。拡張機能のコストです。

    * **[ソース コード リポジトリ]** 。ソース コードへのリンクをコミュニティと共有できます。

    * **[拡張機能に関する Q&A を許可]** 。ユーザーは拡張機能のエントリ ページに質問を残すことができます。

9. **[保存してアップロード]** をクリックします。 このオプションを選択すると、公開元の管理ページに戻ります。 拡張機能はまだ公開されていません。

10. 拡張機能を公開するには、拡張機能を右クリックして **[公開]** を選択します。 Visual Studio Marketplace における拡張機能の表示を確認するには、 **[拡張機能の表示]** を選択します。 取得番号を確認するには、 **[レポート]** をクリックします。 拡張機能に変更を加えるには、 **[編集]** をクリックします。

    ![拡張機能のエントリ メニュー](media/extension-entry-menu.png)

11. **[公開]** をクリックします。これで、拡張機能が公開されます。 Visual Studio Marketplace で拡張機能を検索します。

## <a name="update-a-published-extension-in-visual-studio-marketplace"></a>Visual Studio Marketplace に公開されている拡張機能を更新する

開始する前に、新しいリリース バージョンの拡張機能がビルドされていること、およびそれが最新の状態であることを確認します。

1.  Web ブラウザーで [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) にアクセスします。

1.  右上隅の **[サインイン]** をクリックし、Microsoft アカウントでサインインします。

    :::image type="content" source="media/marketplace-upload-extension.png" alt-text="ファイル エクスプローラーでアップロードされた拡張機能ファイルを選択している様子を示すスクリーンショット。":::

1.  **[拡張機能の公開]** をクリックし、更新した拡張機能のアップロードに使用する公開元を選択します。

    :::image type="content" source="media/marketplace-select-extension-version.png" alt-text="[拡張機能の公開] リンクが強調表示されている Visual Studio Marketplace のスクリーンショット。":::

1.  更新する拡張機能の横にある 3 つの水平ドットの上にマウス ポインターをおいて、 **[編集]** を選択します。

    :::image type="content" source="media/marketplace-select-extension.png" alt-text="編集する拡張機能を選択している様子を示すスクリーンショット。":::

1.  **[1: 拡張機能をアップロード]** で、VSIX ファイル名の後にある鉛筆アイコンをクリックして、公開されている拡張機能を編集します。

     :::image type="content" source="media/marketplace-edit-extension-details.png" alt-text="鉛筆アイコンをクリックして拡張機能を編集することを示すスクリーンショット。":::

1.  拡張機能の更新済み VSIX ファイルを参照します。 ファイルをクリックして、 **[開く]** をクリックします。

    更新された拡張機能がアップロードされます。

    :::image type="content" source="media/marketplace-upload-extension-notification.png" alt-text="編集済みの拡張機能をアップロードした後に表示されるファイルのアップロード通知を示すスクリーンショット。":::

1. **[2: 拡張機能の詳細を指定]** では、拡張機能の更新の一部の情報が読み取り専用になっているか、拡張機能の *source.extension.vsixmanifest* ファイルから自動的に入力されています。 以下に、拡張機能の詳細を示します。

    - **[内部名]** \*。拡張機能の詳細ページの URL で使用されます。 たとえば、公開元名 "myname" で拡張機能を公開し、"my extension" という内部名を指定すると、拡張機能の詳細ページの URL が "marketplace.visualstudio.com/items?itemName=myname.myextension" になります。

    - **[表示名]** \*。拡張機能の表示名です。 この名前は、*source.extension.vsixmanifest* ファイルから自動的に入力されます。

    - **[バージョン番号]** \*。アップロードする拡張機能のバージョン番号です。 このバージョンは、*source.extension.vsixmanifest* ファイルから自動的に入力されます。

    - **[VSIX ID]** \*。Visual Studio で拡張機能に使用される一意識別子です。 拡張機能が自動更新されるようにする場合、この識別子が必要です。 この識別子は、*source.extension.vsixmanifest* ファイルから自動的に入力されます。

    - **[ロゴ]** \*。拡張機能に使用されます。 このロゴは、*source.extension.vsixmanifest* ファイルから自動的に入力されます (指定されている場合)。

    - **[簡単な説明]** \*。拡張機能の動作に関する簡単な説明です。 この説明は、*source.extension.vsixmanifest* ファイルから自動的に入力されます。

    - **[概要]** 。拡張機能の動作のスクリーンショットおよび詳細な情報を入力します。

    - **[サポートされている Visual Studio のバージョン]** \*。拡張機能が動作する Visual Studio のバージョンを選択できます。 拡張機能は、これらのバージョンにのみインストールされます。

    - **[サポートされている Visual Studio のエディション]** \*。拡張機能が動作する Visual Studio のエディションを選択できます。 拡張機能は、これらのエディションにのみインストールされます。

    - **[種類]** 。 最も一般的な拡張機能の種類は **ツール** です。

    - **[カテゴリ]** 。 拡張機能に最適なものを 3 つまで選択できます。

    - **[タグ]** 。ユーザーが拡張機能を検索するのに役立つキーワードです。 タグを使用すると、Visual Studio Marketplace で拡張機能が見つかる可能性が高くなります。

    - **[価格カテゴリ]** 。拡張機能のコストです。

    - **[ソース コード リポジトリ]** 。ソース コードへのリンクをコミュニティと共有できます。

    - **[拡張機能に関する Q&A を許可]** 。ユーザーは拡張機能のエントリ ページに質問を残すことができます。

       \*この詳細は、拡張機能の更新では変更できません。

1. **[保存してアップロード]** をクリックします。 このオプションを選択すると、公開元の管理ページに戻ります。 拡張機能はまだ公開されていません。

1. 拡張機能を公開するには、拡張機能を右クリックして **[公開]** を選択します。 Visual Studio Marketplace における拡張機能の表示を確認するには、 **[拡張機能の表示]** を選択します。 取得番号を確認するには、 **[レポート]** をクリックします。 拡張機能に変更を加えるには、 **[編集]** をクリックします。

## <a name="add-additional-users-to-manage-your-publisher-account"></a>公開元アカウントを管理するユーザーを追加する

Visual Studio Marketplace では、公開元のアカウントにアクセスして管理するためのアクセス許可を別のユーザーに付与することができます。

1. ユーザーを追加する公開元のアカウントに移動します。

2. **[メンバー]** を選択して、 **[追加]** をクリックします。

   ![ユーザーを追加する](media/add-users.png)

3. 次に、追加するユーザーのメール アドレスを指定し、 **[ロールの選択]** で適切なレベルのアクセス許可を付与することができます。  次のオプションから選択できます。

   * **[作成者]** : ユーザーは拡張機能を公開できますが、他のユーザーが公開した拡張機能の表示や管理はできません。

   * **[閲覧者]** : ユーザーは拡張機能を表示できますが、拡張機能の公開や管理はできません。

   * **[共同作成者]** : ユーザーは拡張機能の公開と管理ができますが、公開元設定の編集やアクセスの管理はできません。

   * **[所有者]** : ユーザーは拡張機能の公開と管理、公開元設定の編集、ならびにアクセスの管理ができます。

## <a name="install-the-extension-from-visual-studio-marketplace"></a>Visual Studio Marketplace から拡張機能をインストールする

拡張機能が公開されたので、それを Visual Studio にインストールしてテストします。

1. Visual Studio の **[ツール]** メニューで、 **[拡張機能と更新プログラム]** をクリックします。

2. **[オンライン]** をクリックして、**TestPublish** を検索します。

3. **[Download]** をクリックします。 これで、拡張機能がインストール対象としてスケジュールされます。

4. インストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。

## <a name="remove-the-extension"></a>拡張機能を削除する

Visual Studio Marketplace およびコンピューターから拡張機能を削除できます。

### <a name="to-remove-the-extension-from-visual-studio-marketplace"></a>Visual Studio Marketplace から拡張機能を削除するには

1. [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) にアクセスします。

2. 右上隅の **[拡張機能の公開]** をクリックします。 **TestPublish** の公開に使用した公開元を選択します。 **TestPublish** の一覧が表示されます。

3. 拡張機能のエントリを右クリックし、 **[削除]** をクリックします。 拡張機能を削除するかどうかを確認するメッセージが表示されます。 **[OK]** をクリックします。

### <a name="to-remove-the-extension-from-your-computer"></a>コンピューターから拡張機能を削除するには

1. Visual Studio の **[ツール]** メニューで、 **[拡張機能と更新プログラム]** をクリックします。

2. **[TestPublish]** を選択して、 **[アンインストール]** をクリックします。 これで、拡張機能がアンインストール対象としてスケジュールされます。

3. アンインストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。
