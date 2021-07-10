---
title: Visual Studio 手順 2 のビューおよびページ テンプレートでは、Django のチュートリアルについて説明します
titleSuffix: ''
description: Visual Studio プロジェクトのコンテキストにおける Django の基本のチュートリアルです。具体的には、アプリの作成およびビューとテンプレートの使用に関する手順について取り上げます。
ms.date: 11/19/2018
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18, SEO-VS-2020
ms.workload:
- python
- data-science
ms.openlocfilehash: 196b15dff25681a23c05118a02f19109e09e3959
ms.sourcegitcommit: 5fe2462ffc33c7ece9cf3a179fb598354c916e1f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2021
ms.locfileid: "110320473"
---
# <a name="step-2-create-a-django-app-with-views-and-page-templates"></a>手順 2: ビューおよびページ テンプレートを使用して Django アプリを作成する

**前の手順:[Visual Studio プロジェクトとソリューションを作成する](learn-django-in-visual-studio-step-01-project-and-solution.md)**

現在 Visual Studio プロジェクトにあるのは、1 つ以上の Django *アプリ* を実行できる Django *プロジェクト* のサイトレベル要素だけです。 次の手順では、単一のページを持つ最初のアプリを作成します。

この手順では、次の方法を学習します。

> [!div class="checklist"]
> - 単一のページを持つ Django アプリを作成する (手順 2-1)
> - Django プロジェクトからアプリを実行する (手順 2-2)
> - HTML を使用してビューを表示する (手順 2-3)
> - Django ページ テンプレートを使用してビューを表示する (手順 2-4)

## <a name="step-2-1-create-an-app-with-a-default-structure"></a>手順 2-1: 既定の構造を備えたアプリを作成する

Django アプリは、特定の目的のために関連ファイルのセットを含む別個の Python パッケージです。 Django プロジェクトには、任意の数のアプリを含めることができます。このことは、Web ホストが単一のドメイン名から任意の数の別箇のエントリ ポイントを提供できるという事実を表しています。 たとえば、contoso.com のようなドメインに対する Django プロジェクトには、`www.contoso.com` に 1 つ目のアプリ、support.contoso.com に 2 つ目のアプリ、docs.contoso.com に 3 つ目のアプリを含めることが可能です。 この場合、Django プロジェクトがサイトレベル URL のルーティングと設定 (プロジェクトの *urls.py* および *settings.py* ファイル内) を処理する一方で、各アプリは内部ルーティング、ビュー、モデル、静的ファイル、管理インターフェイスを使って、そのアプリ独自の個々のスタイル設定や動作を保持します。

通常、Django アプリは、標準的なファイル セットから始まります。 次に示すように、Visual Studio では Django プロジェクト内にある Django アプリを初期化する項目テンプレートを提供しています。また、同様の目的を果たす統合メニュー コマンドもあります。

- テンプレート: **ソリューション エクスプローラー** で、プロジェクトを右クリックし、 **[追加]**  >  **[新しい項目]** を選択します。 **[新しい項目の追加]** ダイアログで、**Django 1.9 アプリ** テンプレートを選択し、 **[名前]** フィールドにアプリ名を指定して、 **[OK]** を選択します。

- 統合されたコマンド: **ソリューション エクスプローラー** で、プロジェクトを右クリックし、 **[追加]**  >  **[Django アプリ]** を選択します。 このコマンドでは、名前の入力を要求して、Django 1.9 アプリを作成します。

    ![Django アプリを追加するためのメニュー コマンド](media/django/step02-add-django-app-command.png)

どちらかの方法を使って、"HelloDjangoApp" という名前のアプリを作成します。 結果として、プロジェクト内にこの名前のフォルダーが表示されます。フォルダーには、次の表に示す項目が含まれています。

![ソリューション エクスプローラーでの Django アプリ ファイル](media/django/step02-django-app-in-solution-explorer.png)

::: moniker range="vs-2017"
| アイテム | 説明 |
| --- | --- |
| **\_\_init\_\_.py** | アプリをパッケージとして識別するファイル。 |
| **migrations** | Django が、モデルに対する変更に沿ってデータベースを更新するスクリプトを格納するためのフォルダー。 Django の移行ツールは、現在のモデルに適合するように、データベースの任意の以前のバージョンに必要な変更を適用します。 移行を使用して、モデルにフォーカスを保持し、Django が基になるデータベース スキーマを処理できるようにします。 移行については手順 6 で説明します。ここでは、フォルダーには単に *\_\_init\_\_.py* ファイル (フォルダーが独自の Python パッケージを定義していることを示す) が含まれています。 |
| **templates** | アプリ名に一致するフォルダー内に単純なファイル *index.html* を含む Django ページ テンプレートのフォルダー。 (Visual Studio 2017 15.7 以前の場合、ファイルは *[テンプレート]* のすぐ下に含まれます。手順 2-4 には、サブフォルダーを作成するための指示があります。)テンプレートは、ビューが動的にページを表示するための情報を追加できる HTML のブロックです。 *index.html* 内の `{{ content }}` のようなページ テンプレート "変数" は、この記事で後述する動的な値のプレースホルダーです (手順 2)。 通常、Django アプリは、アプリと名前が一致するサブフォルダーにテンプレートを配置することで、テンプレートの名前空間を作成します。 |
| **admin.py** | アプリの管理インターフェイス (手順 6 を参照) を拡張する Python ファイル。データベース内のデータをシードして編集するために、使用されます。 最初は、このファイルにはステートメント `from django.contrib import admin` のみが含まれています。 既定では、Django には、Django プロジェクトの *settings.py* ファイルにあるエントリを介して標準の管理インターフェイスが含まれています。これらは、*urls.py* の既存のエントリのコメントを解除することで、有効にできます。 |
| **apps.py** | アプリの構成クラスを定義する Python ファイル (この表の後に、以下を参照してください)。 |
| **models.py** | モデルとは、関数によって識別され、ビューがアプリの基本のデータベースを操作するために利用するデータ オブジェクトです (手順 6 を参照)。 アプリがこれらの詳細との関連付けを行う必要がないように、Django はデータベース接続層を提供します。 *models.py* ファイルはモデルを作成するための既定の場所であり、最初はステートメント `from django.db import models` のみを含みます。 |
| **tests.py** | 単体テストの基本構造を含む Python ファイル。 |
| **views.py** | ビューは、通常は Web ページと見なされるものであり、HTTP 要求を取得して HTTP 応答を返します。 一般的に、ビューは Web ブラウザーが表示方法を認識している HTML として表示されますが、ビューが必ずしも表示可能である必要はありません (中間フォームなど)。 ビューは、HTML を表示してブラウザーに送信する役割を担う Python 関数によって定義されています。 *views.py* ファイルはビューを作成するための既定の場所であり、最初はステートメント `from django.shortcuts import render` のみを含みます。 |
::: moniker-end

::: moniker range=">=vs-2019"
| アイテム | 説明 |
| --- | --- |
| **\_\_init\_\_.py** | アプリをパッケージとして識別するファイル。 |
| **migrations** | Django が、モデルに対する変更に沿ってデータベースを更新するスクリプトを格納するためのフォルダー。 Django の移行ツールは、現在のモデルに適合するように、データベースの任意の以前のバージョンに必要な変更を適用します。 移行を使用して、モデルにフォーカスを保持し、Django が基になるデータベース スキーマを処理できるようにします。 移行については [Django ドキュメント](https://docs.djangoproject.com/en/3.2/topics/migrations/)で説明します。ここでは、フォルダーには単に *\_\_init\_\_.py* ファイル (フォルダーが独自の Python パッケージを定義していることを示す) が含まれています。 |
| **templates** | アプリ名に一致するフォルダー内に単純なファイル *index.html* を含む Django ページ テンプレートのフォルダー。 (Visual Studio 2017 15.7 以前の場合、ファイルは *[テンプレート]* のすぐ下に含まれます。手順 2-4 には、サブフォルダーを作成するための指示があります。)テンプレートは、ビューが動的にページを表示するための情報を追加できる HTML のブロックです。 *index.html* 内の `{{ content }}` のようなページ テンプレート "変数" は、この記事で後述する動的な値のプレースホルダーです (手順 2)。 通常、Django アプリは、アプリと名前が一致するサブフォルダーにテンプレートを配置することで、テンプレートの名前空間を作成します。 |
| **admin.py** | アプリの管理インターフェイスを拡張する Python ファイル。データベース内のデータをシードして編集するために、使用されます。 最初は、このファイルにはステートメント `from django.contrib import admin` のみが含まれています。 既定では、Django には、Django プロジェクトの *settings.py* ファイルにあるエントリを介して標準の管理インターフェイスが含まれています。これらは、*urls.py* の既存のエントリのコメントを解除することで、有効にできます。 |
| **apps.py** | アプリの構成クラスを定義する Python ファイル (この表の後に、以下を参照してください)。 |
| **models.py** | モデルは、ビューがアプリの基礎となるデータベースとやりとりするための、関数によって識別されるデータ オブジェクトです。 アプリがこれらの詳細との関連付けを行う必要がないように、Django はデータベース接続層を提供します。 *models.py* ファイルはモデルを作成するための既定の場所であり、最初はステートメント `from django.db import models` のみを含みます。 |
| **tests.py** | 単体テストの基本構造を含む Python ファイル。 |
| **views.py** | ビューは、通常は Web ページと見なされるものであり、HTTP 要求を取得して HTTP 応答を返します。 一般的に、ビューは Web ブラウザーが表示方法を認識している HTML として表示されますが、ビューが必ずしも表示可能である必要はありません (中間フォームなど)。 ビューは、HTML を表示してブラウザーに送信する役割を担う Python 関数によって定義されています。 *views.py* ファイルはビューを作成するための既定の場所であり、最初はステートメント `from django.shortcuts import render` のみを含みます。 |
::: moniker-end

"HelloDjangoApp" という名前を使用した場合、*apps.py* の内容は次のようになります。

```python
from django.apps import AppConfig

class HelloDjangoAppConfig(AppConfig):
    name = 'HelloDjango'
```

### <a name="question-is-creating-a-django-app-in-visual-studio-any-different-from-creating-an-app-on-the-command-line"></a>質問:Visual Studio で Django アプリを作成することは、コマンド ラインでアプリを作成することと、どう違うのですか。

回答:Django アプリ テンプレートを使って、 **[追加]**  >  **[Django アプリ]** コマンドを実行するか、または **[追加]**  >  **[新しい項目]** を使用すると、Django コマンド `manage.py startapp <app_name>` の場合と同じファイルが作成されます。 Visual Studio でアプリを作成することの利点は、アプリ フォルダーとその中のすべてのファイルが自動的にプロジェクトに統合されることです。 同じ Visual Studio コマンドを使用して、プロジェクト内に任意の数のアプリを作成できます。

## <a name="step-2-2-run-the-app-from-the-django-project"></a>手順 2-2: Django プロジェクトからアプリを実行する

この時点で、Visual Studio のプロジェクトをもう一度実行すると (ツール バー ボタンまたは **[デバッグ]**  >  **[デバッグの開始]** を使用)、まだ既定のページが表示されます。 アプリ固有のページを定義し、アプリを Django プロジェクトに追加する必要があるため、アプリのコンテンツは表示されません。

1. *HelloDjangoApp* フォルダーで、以下のコードに合わせて *views.py* を変更します。コードでは、"index" という名前のビューを定義しています。

    ```python
    from django.shortcuts import render
    from django.http import HttpResponse

    def index(request):
        return HttpResponse("Hello, Django!")
    ```

1. *BasicProject* フォルダー (手順 1 で作成済み) で、少なくとも以下のコードに合わせて *urls.py* を変更します (お好みに合わせて、指示コメントはそのままにしておいてもかまいません)。

    ```python
    from django.conf.urls import include, url
    import HelloDjangoApp.views

    # Django processes URL patterns in the order they appear in the array
    urlpatterns = [
        url(r'^$', HelloDjangoApp.views.index, name='index'),
        url(r'^home$', HelloDjangoApp.views.index, name='home'),
    ]
    ```

    各 URL パターンは、Django が固有のサイト相対 URL (つまり、`https://www.domain.com/` に続く部分) のルーティング先にするビューを示します。 正規表現 `^$` から始まる `urlPatterns` の最初のエントリは、サイト ルート "/" に対するルーティングです。 2 つ目のエントリである `^home$` は、明示的に "/home" をルーティングします。 同じビューに対して任意の数のルーティングを保持できます。

1. もう一度プロジェクトを実行すると、ビューに定義されたとおり、**Hello, Django!** という メッセージが表示されます。 完了したら、サーバーを停止します。

### <a name="commit-to-source-control"></a>ソース管理へのコミット

コードに変更を加え、テストが正常に終了したので、このタイミングで、変更を確認してソース管理に追加します。 このチュートリアルの以降の手順で、ソース管理にコミットする適切なタイミングについてもう一度触れる機会があるので、このセクションに戻って参照してください。

1. Visual Studio の下部にある変更ボタン (以下の円印) を選択すると、**チーム エクスプローラー** に移動します。

    ![Visual Studio ステータス バーにあるソース管理の変更ボタン](media/django/step02-source-control-changes-button.png)

1. **チーム エクスプローラー** で "最初の Django アプリの作成" などのコミット メッセージを入力して、 **[Commit All]\(すべてコミットする\)** を選択します。 コミットが完了したら、" **\<hash> のコミットがローカルで作成されました。変更をサーバーと共有するには、同期を使用してください。** " というメッセージが表示されます。 リモート リポジトリに変更をプッシュする場合は、 **[同期]** を選択して、 **[出力方向のコミット]** にある **[プッシュ]** を選択します。 リモートにプッシュする前に、複数のローカル コミットを蓄積しておくことも可能です。

    ![チーム エクスプローラーでリモートにコミットをプッシュする](media/django/step02-source-control-push-to-remote.png)

### <a name="question-what-is-the-r-prefix-before-the-routing-strings-for"></a>質問:ルーティング文字列の前にある 'r' というプレフィックスは何のためにあるのですか。

回答:Python の文字列にある 'r' プレフィックスは "raw" (生) という意味で、文字列内のどの文字もエスケープしないよう Python に指示しています。 正規表現には多くの特殊文字が使用されるため、'r' プレフィックスの使用によって、多くの '\\' エスケープ文字を含むよりもずっと文字列が読みやすくなります。

### <a name="question-what-do-the--and--characters-mean-in-the-url-routing-entries"></a>質問:URL ルーティング エントリでは、^ および $ 文字にどのような意味がありますか。

回答:URL パターンを定義する正規表現では、^ は "行の開始" を意味し、$ は "行の終了" を意味します。ここでも、URL はサイト ルートへの相対 (`https://www.domain.com/` の後に続く部分) です。 正規表現 `^$` は効果的に "空白" を意味するため、完全な URL `https://www.domain.com/` (サイト ルートに何も追加されない) と一致します。 パターン `^home$` は `https://www.domain.com/home/` と完全に一致します (Django では、パターン マッチングに末尾の / を使用しません)。

`^home` のように、正規表現で末尾の $ を使用しない場合、URL パターンは "home"、"homework"、"homestead"、および "home192837" など、"home" で始まる *任意* の URL と一致します。

別の正規表現を使って実験するには、[pythex.org](https://www.pythex.org) で [regex101.com](https://regex101.com) のようなオンライン ツールを試行してください。

## <a name="step-2-3-render-a-view-using-html"></a>手順 2-3: HTML を使用してビューを表示する

*views.py* に既にある `index` 関数では、ページに対するプレーンテキストの HTTP 応答以外は生成されません。 もちろん、現実のほとんどの Web ページは、ライブ データを頻繁に取り込む豊富な HTML ページを使って応答します。 実際、関数を使用してビューを定義する主な理由は、ビューのコンテンツを動的に生成できるからです。

`HttpResponse` の引数は単に文字列なので、文字列内に自由に HTML を構築できます。 単純な例としては、`index` 関数を次のコード (既存の `from` ステートメントを保持する) に置き換えます。これにより、ページを更新するたびに更新される動的コンテンツを使用する HTML 応答が生成されます。

```python
from datetime import datetime

def index(request):
    now = datetime.now()

    html_content = "<html><head><title>Hello, Django</title></head><body>"
    html_content += "<strong>Hello Django!</strong> on " + now.strftime("%A, %d %B, %Y at %X")
    html_content += "</body></html>"

    return HttpResponse(html_content)
```

もう一度プロジェクトを実行すると、"**Hello Django!** on Monday, 16 April, 2018 at 16:28:10"\(ようこそ、Django へ! 2018 年 4 月 16 日、月曜日の 16 時 28 分 10 秒\)" のようなメッセージが表示されます。 ページを更新すると時間が更新され、各要求によってコンテンツが生成されていることを確認できます。 完了したら、サーバーを停止します。

> [!Tip]
> プロジェクトの停止および再起動を行う簡単な方法として、 **[デバッグ]**  >  **[再起動]** メニュー コマンド (**Ctrl**+**Shift**+**F5** キー) を使用するか、または以下のデバッグ ツールバーの **[再起動]** ボタンを使用します。
>
> ![Visual Studio のデバッグ ツールバーにある再起動ボタン](media/debugging-restart-toolbar-button.png)

## <a name="step-2-4-render-a-view-using-a-page-template"></a>手順 2-4: ページ テンプレートを使用してビューを表示する

コードでの HTML の生成は、非常に小規模なページでは問題ありませんが、ページが複雑になると、通常は、ぺ―ジの静的な HTML 部分を "ページ テンプレート" として (CSS および JavaScript ファイルへの参照と併せて) 保守し、そこに動的なコード生成コンテンツを挿入したいと考えます。 前のセクションでは、`now.strftime` 呼び出しの日時のみが動的であり、それ以外のすべての内容はページ テンプレートに配置できることを意味します。

Django ページ テンプレートは、`{{ content }}` 内と同様に、`{{` や `}}` で区切られる "変数" という任意の数の置換トークンを含むことができる HTML のブロックです。 Django のテンプレート モジュールは、コードで提供した動的コンテンツで変数を置き換えます。

ページ テンプレートを使用する手順を次に示します。

1. Django プロジェクトが格納されている *BasicProject* フォルダーの *settings.py* ファイルを開き、アプリ名 "HelloDjangoApp" を `INSTALLED_APPS` 一覧に追加します。 アプリを一覧に追加すると、アプリを格納しているこの名前のフォルダーがあることが、Django プロジェクトに通知されます。

    ```python
    INSTALLED_APPS = [
        'HelloDjangoApp',
        # Other entries...
    ]
    ```

1. また、*settings.py* で、`TEMPLATES` オブジェクトに以下の行 (既定で組み込まれている) が含まれていることを確認します。この行は、インストールされたアプリの *templates* フォルダー内でテンプレートを検索するよう Django に指示します。

    ```json
    'APP_DIRS': True,
    ```

1. *HelloDjangoApp* フォルダーの *templates/HelloDjangoApp/index.html* ページ テンプレート ファイル (VS 2017 15.7 以前の場合、*templates/index.html*) を開き、`{{ content }}` という 1 つの変数が含まれていることを確認します。

    ```html
    <html>
    <head><title></title></head>

    <body>

    {{ content }}

    </body>
    </html>
    ```

1. *HelloDjangoApp* フォルダーの *views.py* を開き、`index` 関数を `django.shortcuts.render` ヘルパー関数を使用する次のコードに置き換えます。 `render` ヘルパーは、ページ テンプレートを操作するために簡素化されたインターフェイスを提供しています。 必ず、すべての既存の `from` ステートメントをそのまま保持します。

    ```python
    from django.shortcuts import render   # Added for this step

    def index(request):
        now = datetime.now()

        return render(
            request,
            "HelloDjangoApp/index.html",  # Relative path from the 'templates' folder to the template file
            # "index.html", # Use this code for VS 2017 15.7 and earlier
            {
                'content': "<strong>Hello Django!</strong> on " + now.strftime("%A, %d %B, %Y at %X")
            }
        )
    ```

    見てわかるように、`render` の最初の引数は要求オブジェクトであり、その後ろにはアプリの *templates* フォルダー内の一時ファイルへの相対パスが続きます。 必要に応じて、ビューに対応する名前を付けたテンプレートがサポートされます。 `render` の 3 つ目の引数は、テンプレートが参照する変数のディクショナリです。 テンプレートの変数が `{{ object.property }}` を参照できる場合、ディクショナリにオブジェクトを含めることができます。

1. プロジェクトを実行して、出力を確認します。 手順 2-2 で確認したものとほぼ同じメッセージが表示され、テンプレートが機能していることが示されます。

    ただし、`content` プロパティで使用した HTML がプレーン テキストとしてのみ表示されることを確認してください。`render` 関数は自動的にこの HTML をエスケープするためです。 自動エスケープによって、インジェクション攻撃に対する偶発的な脆弱性を防ぎます。開発者は、1 つのページから入力を収集し、テンプレートのプレースホルダーを介して別のページの値として使用することがよくあります。 エスケープは、HTML をコードとは別にページ テンプレートに保存する方法が最善であることを思い出すためにも役立ちます。 幸いにも、必要に応じて追加の変数を作成することは簡単です。 たとえば、以下のマークアップに合うように *テンプレート* で *index.html* を変更します。これにより、ページ タイトルが追加され、ページ テンプレートのすべての書式設定がそのまま保持されます。

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
        </head>
        <body>
            <strong>{{ message }}</strong>{{ content }}
        </body>
    </html>
    ```

    次に、ページ テンプレートのすべての変数の値を指定するために、`index` ビュー関数を以下のように記述します。

    ```python
    def index(request):
        now = datetime.now()

        return render(
            request,
            "HelloDjangoApp/index.html",  # Relative path from the 'templates' folder to the template file
            # "index.html", # Use this code for VS 2017 15.7 and earlier
            {
                'title' : "Hello Django",
                'message' : "Hello Django!",
                'content' : " on " + now.strftime("%A, %d %B, %Y at %X")
            }
        )
    ```

1. サーバーを停止し、プロジェクトを再起動して、以下のようにページが適切に表示されることを確認します。

    ![テンプレートを使用してアプリを実行する](media/django/step02-result.png)

1. <a name="template-namespacing"></a>Visual Studio 2017 バージョン 15.7 以前: 最後の手順として、アプリと同じ名前のサブフォルダーにテンプレートを移動します。これにより、名前空間が作成され、プロジェクトに追加する可能性がある他のアプリとの潜在的な競合が回避されます。 (VS 2017 15.8+ のテンプレートはこれを自動的に行います。)つまり、*templates* に *HelloDjangoApp* という名前のサブフォルダーを作成し、そのサブフォルダーに *index.html* を移動して、テンプレートの新しいパスである *HelloDjangoApp/index.html* を参照するように `index` ビュー関数を変更します。 次に、プロジェクトを実行してページが正しく表示されることを確認し、サーバーを停止します。

1. ソース管理への変更をコミットし、必要に応じて[手順 2-2](#commit-to-source-control) の説明に従って、リモート リポジトリを更新します。

### <a name="question-do-page-templates-have-to-be-in-a-separate-file"></a>質問:ページ テンプレートを別のファイルにする必要はありますか。

回答:通常、テンプレートは別の HTML ファイルで保持されていますが、インライン テンプレートも使用できます。 ただし、マークアップとコード間の明確な分離を維持するために、別個のファイルを使用することが推奨されています。

### <a name="question-must-templates-use-the-html-file-extension"></a>質問:テンプレートには、.html ファイルの拡張子を使用する必要がありますか。

回答:`render` 関数の 2 つ目の引数にファイルへの正確な相対パスを常に指定するため、ページ テンプレート ファイルの *.html* 拡張子は完全にオプションです。 ただし、Visual Studio (および、その他のエディター) では通常、 *.html* ファイルでのコード補完や構文の色付けなどの機能を提供しており、このことは、ページ テンプレートが厳密に HTML ではないという事実よりも重要です。

実際に、Django プロジェクトを操作していると、Visual Studio では、編集中の HTML ファイルが実際には Django テンプレートである場合を自動検出して、特定のオートコンプリート機能を提供します。 たとえば、Django ページ テンプレートのコメント　`{#` の入力を開始すると、Visual Studio では終了の `#}` 文字を自動的に提示します。 また、 **[選択範囲のコメント]** および **[選択範囲のコメントを解除]** コマンド ( **[編集]**  >  **[詳細]** メニューおよびツールバー上にある) では、HTML コメントではなく、テンプレート コメントを使用します。

### <a name="question-when-i-run-the-project-i-see-an-error-that-the-template-cannot-be-found-whats-wrong"></a>質問:プロジェクトを実行すると、テンプレートが見つからないというエラーが表示されます。 理由

回答:テンプレートが見つからないというエラーが表示される場合は、アプリを `INSTALLED_APPS` 一覧にある Django プロジェクトの *settings.py* に追加済みであることを確認してください。 そのエントリがない場合、Django ではアプリの *templates* フォルダー内の検索が認識されません。

### <a name="question-why-is-template-namespacing-important"></a>質問:どうして、テンプレートの名前空間の設定が重要なのですか。

回答:Django が `render` 関数で参照されるテンプレートを検索するとき、相対パスに一致する最初に検出した任意のファイルを使用します。 テンプレートに同じフォルダー構造を使用している複数の Django アプリが、同じプロジェクト内にある場合、1 つのアプリが意図せずに、もう 1 つのアプリのテンプレートを使用します。 このようなエラーを回避するために、アプリの *templates* フォルダー内にアプリ名と一致するサブフォルダーを必ず作成して、あらゆる重複を防止してください。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [静的ファイルを提供し、ページを追加し、テンプレート継承を使用する](learn-django-in-visual-studio-step-03-serve-static-files-and-add-pages.md)

## <a name="go-deeper"></a>詳しい説明

- [最初の Django アプリの作成、パート 1 - ビュー](https://docs.djangoproject.com/en/2.0/intro/tutorial01/#write-your-first-view) (docs.djangoproject.com)
- インクルードと継承など Django テンプレートの詳細な機能について、「[The Django template language](https://docs.djangoproject.com/en/2.0/ref/templates/language/)」(Django テンプレート言語) (docs.djangoproject.com) を確認する
- [inLearning での正規表現のトレーニング](https://www.linkedin.com/learning/topics/regular-expressions) (LinkedIn)
- GitHub のチュートリアルのソース コード:[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
