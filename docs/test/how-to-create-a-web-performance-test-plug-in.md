---
title: Web パフォーマンス テスト プラグインを作成する
ms.date: 10/03/2016
ms.topic: conceptual
f1_keywords:
- vs.test.web.webtestplugin
helpviewer_keywords:
- Web performance tests, creating plug-ins
- plug-ins, creating in Web performance tests
ms.assetid: a612f2d2-9806-477d-a126-12842f07da6e
author: gewarren
ms.author: gewarren
manager: jillfra
ms.prod: visual-studio-dev15
ms.openlocfilehash: 34e9358dbe84f93e107a28298e6657df801ea6f6
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54938946"
---
# <a name="how-to-create-a-web-performance-test-plug-in"></a>方法: Web パフォーマンス テスト プラグインを作成する

Web パフォーマンス テスト プラグインを使用すると、Web パフォーマンス テストの主要な宣言ステートメントとコードを分離し、そのコードを再利用できます。 カスタマイズされた Web パフォーマンス テスト プラグインには、Web パフォーマンス テストの実行時に一部のコードを呼び出す方法が用意されています。 Web パフォーマンス テスト プラグインは、テスト イテレーションごとに 1 回実行されます。 また、テスト プラグインで PreRequest メソッドまたは PostRequest メソッドをオーバーライドすると、これらの要求プラグインは各要求のそれぞれ前または後に実行されます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

カスタマイズされた Web パフォーマンス テスト プラグインは、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin> 基底クラスから独自のクラスを派生することによって作成できます。

記録した Web パフォーマンス テストではカスタマイズされた Web パフォーマンス テスト プラグインを使用できるため、最小限のコードを記述するだけで、Web パフォーマンス テストをより高度に制御できるようになります。 ただし、コード化された Web パフォーマンス テストでそれらを使用することもできます。 詳細については、「[Generate and run a coded web performance test](../test/generate-and-run-a-coded-web-performance-test.md)」(コード化された Web パフォーマンス テストの生成と実行) を参照してください。

> [!NOTE]
> ロード テスト プラグインも作成できます。「[方法: ロード テスト プラグインを作成する](../test/how-to-create-a-load-test-plug-in.md)」を参照してください。

## <a name="to-create-a-custom-web-performance-test-plug-in"></a>カスタム Web パフォーマンス テスト プラグインを作成するには

1.  Web パフォーマンス テストが含まれている、Web パフォーマンスとロード テストのプロジェクトを開きます。

2.  **ソリューション エクスプローラー**で、ソリューションを右クリックし、**[追加]** を選択して、**[新しいプロジェクト]** を選択します。

     **[新しいプロジェクトの追加]** ダイアログ ボックスが表示されます。

3.  **[インストールされているテンプレート]** の **[Visual C#]** を選択します。

4.  テンプレートの一覧で、**[クラス ライブラリ]** を選択します。

5.  **[名前]** ボックスに、クラスの名前を入力します。

6.  **[OK]** をクリックします。

7.  新しいクラス ライブラリ プロジェクトが**ソリューション エクスプローラー**に追加され、新しいクラスが**コード エディター**に表示されます。

8.  **ソリューション エクスプローラー**で、新しいクラス ライブラリの **[参照設定]** フォルダーを右クリックし、**[参照の追加]** を選択します。

9. **[参照の追加]** ダイアログ ボックスが表示されます。

10. **[.NET]** タブを選択し、スクロール ダウンして **[Microsoft.VisualStudio.QualityTools.WebTestFramework]** を選択します。

11. **[OK]** をクリックします。

     **Microsoft.VisualStudio.QualityTools.WebTestFramework** への参照が**ソリューション エクスプローラー**内の **[参照設定]** フォルダーに追加されます。

12. **ソリューション エクスプローラー**で、Web パフォーマンス テスト プラグインの追加先であるロード テストを含んでいる Web パフォーマンスおよびロード テスト プロジェクトの最上位ノードを右クリックし、**[参照の追加]** を選択します。

13. **[参照の追加]** ダイアログ ボックスが表示されます。

14. **[プロジェクト]** タブをクリックし、**[クラス ライブラリ プロジェクト]** を選択します。

15. **[OK]** をクリックします。

16. **コード エディター**で、プラグインのコードを記述します。 まず、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin> クラスから派生する新しいパブリック クラスを作成します。

17. 1 つまたは複数のイベント ハンドラー内でコードを実装します。 実装のサンプルについては、次の例を参照してください。

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostWebTestRecordingEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostWebTestEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PreRequestEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostRequestEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PrePageEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostPageEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PreTransactionEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostTransactionEventArgs>

18. このコードを記述した後で、新しいプロジェクトをビルドします。

19. Web パフォーマンス テストを開きます。

20. Web パフォーマンス テスト プラグインを追加するには、ツール バーの **[Web テスト プラグインの追加]** を選択します。

     **[Web テスト プラグインの追加]** ダイアログ ボックスが表示されます。

21. **[プラグインの選択]** で、Web パフォーマンス テスト プラグイン クラスを選択します。

22. **[選択したプラグインのプロパティ]** ペインで、実行時に使用するプラグインの初期値を設定します。

    > [!NOTE]
    > プラグインのプロパティをパブリック、設定可能、および基本型 (整数型、ブール型、文字列型など) として設定して、任意の数だけ公開できます。 Web パフォーマンス テスト プラグインのプロパティは、後で [プロパティ] ウィンドウを使用して変更することもできます。

23. **[OK]** をクリックします。

     **[Web テスト プラグイン]** フォルダーにプラグインが追加されます。

    > [!WARNING]
    > プラグインを使用する Web パフォーマンス テストまたはロード テストを実行すると、次のようなエラー メッセージが表示されることがあります。
    >
    > **要求に失敗しました:\<plug-in> イベントの例外:ファイルまたはアセンブリ '\<"Plug-in name".dll file>, Version=\<n.n.n.n>, Culture=neutral, PublicKeyToken=null' またはその依存関係の 1 つが読み込めませんでした。指定されたファイルが見つかりません。**
    >
    > この問題が発生するのは、いずれかのプラグインのコードを変更して、新しい DLL バージョン **(Version=0.0.0.0)** を作成したのに、プラグインが元のプラグイン バージョンを参照したままになっている場合です。 この問題を解決するには、次の手順を実行します。
    >
    > 1.  Web パフォーマンスとロード テストのプロジェクトで、参照に関する警告が表示されます。 プラグイン DLL への参照を削除し、再度追加します。
    > 2.  プラグインをテストまたは該当する場所から削除し、その後、追加し直します。

## <a name="example"></a>例

次のコードでは、テスト イテレーションを表す <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestContext> に項目を追加する、カスタマイズされた Web パフォーマンス テスト プラグインを作成します。

Web パフォーマンス テストの実行後は、このプラグインを使用することにより、**TestIteratnionNumber** という名前の追加された項目を、**Web パフォーマンス テスト結果ビューアー**の **[コンテキスト]** タブで確認できます。

```csharp
using System;
using System.Collections.Generic;
using System.Text;
using System.ComponentModel;
using Microsoft.VisualStudio.TestTools.WebTesting;

namespace SampleRules
{
    [Description("This plugin can be used to set the ParseDependentsRequests property for each request")]
    public class SampleWebTestPlugin : WebTestPlugin
    {
        private bool m_parseDependents = true;

        public override void PreWebTest(object sender, PreWebTestEventArgs e)
        {
            // TODO: Add code to execute before the test.
        }

        public override void PostWebTest(object sender, PostWebTestEventArgs e)
        {
            // TODO: Add code to execute after the test.
        }

        public override void PreRequest(object sender, PreRequestEventArgs e)
        {
            // Code to execute before each request.
            // Set the ParseDependentsRequests value on the request
            e.Request.ParseDependentRequests = m_parseDependents;
        }

        // Properties for the plugin.
        [DefaultValue(true)]
        [Description("All requests will have their ParseDependentsRequests property set to this value")]
        public bool ParseDependents
        {
            get
            {
                return m_parseDependents;
            }
            set
            {
                m_parseDependents = value;
            }
        }
    }
}
```

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>
- [ロード テスト用のカスタム コードおよびカスタム プラグインの作成](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [方法: 要求レベルのプラグインを作成する](../test/how-to-create-a-request-level-plug-in.md)
- [Web パフォーマンス テストのカスタム抽出規則のコーディング](../test/code-a-custom-extraction-rule-for-a-web-performance-test.md)
- [Web パフォーマンス テストのカスタム検証規則のコーディング](../test/code-a-custom-validation-rule-for-a-web-performance-test.md)
- [方法: ロード テスト プラグインを作成する](../test/how-to-create-a-load-test-plug-in.md)
- [コード化された Web パフォーマンス テストの生成と実行](../test/generate-and-run-a-coded-web-performance-test.md)