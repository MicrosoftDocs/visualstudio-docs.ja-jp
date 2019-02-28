---
title: MSBuild Properties1 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
helpviewer_keywords:
- MSBuild, properties
ms.assetid: 962912ac-8931-49bf-a88c-0200b6e37362
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 104fe082f9e18a7be97f2ab95a022288316cc638
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54773236"
---
# <a name="msbuild-properties1"></a>MSBuild Properties1
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
プロパティはビルドを設定するための名前と値のペアです。 プロパティを使用することで、タスクに値を渡したり、条件を評価したりできるだけでなく、プロジェクト ファイルで参照する値を格納しておくこともできます。  
  
## <a name="defining-and-referencing-properties-in-a-project-file"></a>プロジェクト ファイルでのプロパティの定義と参照  
 プロパティを宣言するには、そのプロパティの名前を持つ要素を [PropertyGroup](../msbuild/propertygroup-element-msbuild.md) 要素の子として作成します。 たとえば、次の XML では、`BuildDir` という名前のプロパティを作成し、`Build` を値として設定しています。  
  
```  
<PropertyGroup>  
    <BuildDir>Build</BuildDir>  
</PropertyGroup>  
```  
  
 プロジェクト ファイルでプロパティを参照するには、$(`PropertyName`) という構文を使用します。 たとえば、前の例に示したプロパティを参照するには、$(BuildDir) と記述します。  
  
 プロパティ値を変更するには、プロパティを再定義します。 `BuildDir` プロパティに新しい値を設定するには、次の XML を使用します。  
  
```  
<PropertyGroup>  
    <BuildDir>Alternate</BuildDir>  
</PropertyGroup>  
```  
  
 プロパティは、プロジェクト ファイルに表示される順に評価されます。 `BuildDir` の新しい値は、古い値が割り当てられた後で宣言する必要があります。  
  
## <a name="reserved-properties"></a>予約済みのプロパティ  
 MSBuild では、プロジェクト ファイルに関する情報や MSBuild のバイナリに関する情報を保持するために、いくつかのプロパティ名が予約されています。 これらのプロパティは、他のプロパティと同じように $ 表記を使用して参照できます。 たとえば、$(MSBuildProjectFile) は、ファイル名の拡張子を含むプロジェクト ファイルの完全なファイル名を返します。  
  
 詳細については、「[方法: プロジェクト ファイルの名前または場所を参照する](../msbuild/how-to-reference-the-name-or-location-of-the-project-file.md)」および「[MSBuild の予約済みおよび既知のプロパティ](../msbuild/msbuild-reserved-and-well-known-properties.md)」を参照してください。  
  
## <a name="environment-properties"></a>環境プロパティ  
 プロジェクト ファイルで環境変数を参照する場合も、予約済みのプロパティを参照するときと同じ方法を使用します。 たとえば、プロジェクト ファイルで `PATH` 環境変数を使用するには、$(Path) と記述します。 プロジェクト ファイルに、環境プロパティと同じ名前のプロパティが定義されている場合、環境変数の値はプロジェクト内のプロパティによってオーバーライドされます。  
  
 各 MSBuild プロジェクトには、分離された環境ブロックがあります。各プロジェクトは独自のブロックに対する読み取りと書き込みのみを参照します。  プロジェクト ファイルの評価やビルドを行う前、MSBuild では、プロパティ コレクションが初期化されるときに環境変数のみを読み取ります。 その後で、環境プロパティは静的なプロパティになります。つまり、起動されたツールは、同じ名前と値で実行が開始されます。  
  
 起動されたツール内から環境変数の現在の値を取得するには、[プロパティ関数](../msbuild/property-functions.md) System.Environment.GetEnvironmentVariable を使用します。 ただし推奨される方法は、タスク パラメーター <xref:Microsoft.Build.Utilities.ToolTask.EnvironmentVariables%2A> を使用する方法です。 この文字列配列に設定されている環境プロパティは、起動されたツールに渡すことができます。このとき、システム環境変数は影響を受けません。  
  
> [!TIP]
>  すべての環境変数が読み取られて、初期プロパティになるわけではありません。 有効な MSBuild プロパティ名 ("386" など) を名前として持っていない環境変数は無視されます。  
  
 詳細については、「[方法: ビルドで環境変数を使用する](../msbuild/how-to-use-environment-variables-in-a-build.md)」を参照してください。  
  
## <a name="registry-properties"></a>レジストリのプロパティ  
 システム レジストリ値を読み取るには、次の構文を使用します。ここで、`Hive` はレジストリ ハイブ (たとえば、HKEY_LOCAL_MACHINE)、`Key` はキー名、`SubKey` はサブキー名、`Value` はサブキーの値をそれぞれ表します。  
  
```  
$(registry:Hive\MyKey\MySubKey@Value)  
```  
  
 既定のサブキー値を取得するには、`Value` を省略します。  
  
```  
$(registry:Hive\MyKey\MySubKey)  
```  
  
 このレジストリ値を使用して、ビルド プロパティを初期化できます。 たとえば、Visual Studio の Web ブラウザーのホーム ページを表すビルド プロパティを作成するには、次のコードを使用します。  
  
```  
<PropertyGroup>  
  <VisualStudioWebBrowserHomePage>  
    $(registry:HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\12.0\WebBrowser@HomePage)  
  </VisualStudioWebBrowserHomePage>  
<PropertyGroup>  
```  
  
## <a name="global-properties"></a>グローバル プロパティ  
 MSBuild では、**/property** (または **/p**) スイッチを使用してコマンド ラインからプロパティを設定できます。 これらのグローバル プロパティ値は、プロジェクト ファイルで設定されたプロパティ値をオーバーライドします。 これには環境プロパティは含まれますが、予約済みのプロパティは含まれません。予約済みのプロパティは変更できません。  
  
 グローバルな `Configuration` プロパティを `DEBUG` に設定する例を次に示します。  
  
```  
msbuild.exe MyProj.proj /p:Configuration=DEBUG  
```  
  
 グローバル プロパティは、MSBuild タスクの `Properties` 属性を使用することで、複数プロジェクトのビルドに含まれる子プロジェクトに対して設定または変更することもできます。 詳細については、「[MSBuild タスク](../msbuild/msbuild-task.md)」を参照してください。  
  
 プロジェクト タグで `TreatAsLocalProperty` 属性を使用してプロパティを指定する場合、そのグローバル プロパティ値は、プロジェクト ファイルで設定されているプロパティ値をオーバーライドしません。 詳細については、「[Project 要素 (MSBuild)](../msbuild/project-element-msbuild.md)」「[How to: Build the Same Source Files with Different Options (方法: 同じソース ファイルを異なるオプションでビルドする)](../msbuild/how-to-build-the-same-source-files-with-different-options.md)」を参照してください。  
  
## <a name="property-functions"></a>プロパティ関数  
 .NET Framework Version 4 以降では、プロパティ関数を使用して MSBuild スクリプトを評価できるようになりました。 MSBuild タスクを使用しなくても、システム時刻の読み取り、文字列の比較、正規表現の照合、その他のさまざまな処理をビルド スクリプト内で実行できます。  
  
 文字列 (インスタンス) メソッドを使用してプロパティ値を操作したり、各種システム クラスの静的メソッドを呼び出したりできます。 たとえば、ビルド プロパティを今日の日付に設定するには、次のようにします。  
  
```  
<Today>$([System.DateTime]::Now.ToString("yyyy.MM.dd"))</Today>  
```  
  
 プロパティ関数の詳細と、プロパティ関数の一覧については、「[プロパティ関数](../msbuild/property-functions.md)」を参照してください。  
  
## <a name="creating-properties-during-execution"></a>実行時のプロパティの作成  
 `Target` 要素の外側にあるプロパティには、ビルドの評価フェーズで値が割り当てられます。 その後の実行フェーズでプロパティを作成または変更するには、次のようにします。  
  
-   プロパティはどのタスクでも生成できます。 プロパティを生成するには、[Task](../msbuild/task-element-msbuild.md) 要素の子要素として、`PropertyName` 属性を持つ [Output](../msbuild/output-element-msbuild.md) 要素を持つ必要があります。  
  
-   プロパティは [CreateProperty](../msbuild/createproperty-task.md) タスクによって生成できます。 この使用法は非推奨とされます。  
  
-   .NET Framework 3.5 以降では、プロパティ宣言を格納できる `Target` 要素を  `PropertyGroup` 要素に含めることができます。  
  
## <a name="storing-xml-in-properties"></a>プロパティに XML を格納する  
 プロパティには、タスクに値を渡したり、ログ情報を表示したりするための任意の XML を格納できます。 次の例では、`ConfigTemplate` プロパティの値に、XML や他のプロパティ参照が使用されています。 このプロパティ参照は、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] により、対応するプロパティ値を使用して置き換えられます。 プロパティ値は表示される順に割り当てられます。 したがって、この例では、`$(MySupportedVersion)`、`$(MyRequiredVersion)`、および `$(MySafeMode)` は既に定義されています。  
  
```  
  
<PropertyGroup>  
    <ConfigTemplate>  
        <Configuration>  
            <Startup>  
                <SupportedRuntime  
                    ImageVersion="$(MySupportedVersion)"  
                    Version="$(MySupportedVersion)"/>  
                <RequiredRuntime  
                    ImageVersion="$(MyRequiredVersion)  
                    Version="$(MyRequiredVersion)"  
                    SafeMode="$(MySafeMode)"/>  
            </Startup>  
        </Configuration>  
    </ConfigTemplate>  
</PropertyGroup>  
```  
  
## <a name="see-also"></a>関連項目
 [MSBuild の概念](../msbuild/msbuild-concepts.md)  
 [MSBuild](msbuild.md)  
 [方法: ビルドで環境変数を使用する](../msbuild/how-to-use-environment-variables-in-a-build.md)   
 [方法: プロジェクト ファイルの名前または場所を参照する](../msbuild/how-to-reference-the-name-or-location-of-the-project-file.md)   
 [方法: 同じソース ファイルを異なるオプションでビルドする](../msbuild/how-to-build-the-same-source-files-with-different-options.md)   
 [MSBuild の予約済みおよび既知のプロパティ](../msbuild/msbuild-reserved-and-well-known-properties.md)   
 [Property 要素 (MSBuild)](../msbuild/property-element-msbuild.md)
