---
title: MSBuild | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, about MSBuild
- MSBuild, overview
ms.assetid: e39f13f7-1e1d-4435-95ca-0c222bca071c
caps.latest.revision: 62
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b204a0f3bda5eab9291d4201fbea3c39a3f62ca6
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60050401"
---
# <a name="msbuild"></a>MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecmsbuildengine](../includes/vstecmsbuildengine-md.md)] は、アプリケーションをビルドするためのプラットフォームです。 MSBuild とも呼ばれるこのエンジンには、ビルド プラットフォームでソフトウェアを処理およびビルドする方法を制御する、プロジェクト ファイル用の XML スキーマが用意されています。 Visual Studio は MSBuild を使用しますが、MSBuild は Visual Studio に依存しません。 プロジェクト ファイルまたはソリューション ファイルに対して msbuild.exe を実行すると、Visual Studio がインストールされていない環境で、製品の統合とビルドを実行できます。  
  
 Visual Studio は、マネージド プロジェクトの読み込みとビルドを行う MSBuild をホストしています。 Visual Studio のプロジェクト ファイル (.csproj、vbproj、vcxproj など) には、IDE を使用してプロジェクトをビルドするときに実行される MSBuild XML コードが含まれています。 Visual Studio プロジェクトには、一般的な開発作業を行う必要なすべての設定とビルド プロセスがインポートされますが、Visual Studio 内のエディターや任意の XML エディターを使用してそれらを拡張または変更することもできます。  
  
 C++ に対する MSBuild の詳細については、「[MSBuild (Visual C++)](http://msdn.microsoft.com/library/7a1be7ff-0312-4669-adf2-5f5bf507d560)」をご覧ください。  
  
 次の例では、Visual Studio IDE の代わりに、MSBuild コマンド ラインでビルドを実行する状況について説明します。  
  
- Visual Studio 2013 がインストールされていません。  
  
- MSBuild の 64 ビット バージョンを使用することを希望しています。 通常は MSBuild のこのバージョンは不要ですが、このバージョンを使用すると、MSBuild はより多くのメモリにアクセスできます。  
  
- 複数のプロセスでビルドを実行することを希望しています。 ただし、C++ および C# で記述したプロジェクトに関しては、同じ結果を達成するために IDE を使用することもできます。  
  
- ビルド システムを変更することを希望しています。 たとえば、次の操作を有効にすることを希望する場合があります。  
  
  - コンパイラに渡す前に、ファイルを前処理します。  
  
  - ビルド出力を別の場所にコピーします。  
  
  - ビルド出力から圧縮ファイルを作成します。  
  
  - 後処理手順を実行します。 たとえば、1 つのアセンブリに対して、異なる複数のバージョンをスタンプとして割り当てることがあります。  
  
  Visual Studio IDE でコードを作成し、MSBuild を使用してビルドを実行することもできます。 別の方法として、開発用コンピューターの IDE でコードをビルドすることもできますが、単一の MSBuild コマンド ラインを使用して、複数の開発者から取得して統合したコードをビルドすることもできます。  
  
> [!NOTE]
>  Team Foundation ビルドを使用して、アプリケーションのコンパイル、テスト、および配置を自動的に実行することもできます。 開発者がコードをチェックインしたとき (たとえば、継続的インテグレーションの手法の一環として)、またはスケジュールに従って (たとえば、夜間のビルド確認テストの一部として)、ビルド システムがビルドを自動的に実行ですることもできます。 Team Foundation ビルドは、MSBuild を使用してコードをコンパイルします。 詳細については、「[アプリケーションのビルド](http://msdn.microsoft.com/library/a971b0f9-7c28-479d-a37b-8fd7e27ef692)」をご覧ください。  
  
 ここでは、MSBuild の概要について説明します。 入門チュートリアルについては、[チュートリアル: MSBuild の使用](../msbuild/walkthrough-using-msbuild.md)に関するページを参照してください。  
  
 **このトピックの内容**  
  
- [コマンド プロンプトでの MSBuild の使用](#BKMK_CommandPrompt)  
  
- [プロジェクト ファイル](#BKMK_ProjectFile)  
  
    - [Properties](#BKMK_Properties)  
  
    - [項目](#BKMK_Items)  
  
    - [タスク](#BKMK_Tasks)  
  
    - [ターゲット](#BKMK_Targets)  
  
- [ビルド ログ](#BKMK_BuildLogs)  
  
- [Visual Studio での MSBuild の使用](#BKMK_VisualStudio)  
  
- [マルチ ターゲット](#BKMK_Multitargeting)  
  
## <a name="BKMK_CommandPrompt"></a> コマンド プロンプトでの MSBuild の使用  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] をコマンド プロンプトで実行するには、MSBuild.exe にプロジェクト ファイルを渡し、適切なコマンド ライン オプションを指定して実行します。 コマンド ライン オプションでは、プロパティを設定したり、特定のターゲットを実行したりできるほか、ビルド処理を制御するその他のオプションも設定できます。 たとえば、`MyProj.proj` プロパティを `Configuration` に設定してファイル `Debug` をビルドするには、次のコマンド ライン構文を使用します。  
  
```  
MSBuild.exe MyProj.proj /property:Configuration=Debug  
```  
  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] のコマンド ライン オプションの詳細については、「[コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)」をご覧ください。  
  
> [!IMPORTANT]
>  プロジェクトをダウンロードする前に、コードが信頼できるものかどうかを確認してください。  
  
## <a name="BKMK_ProjectFile"></a> プロジェクト ファイル  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] では、簡単で拡張性がある XML ベースのプロジェクト ファイル形式が採用されています。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] のプロジェクト ファイル形式では、ビルドする項目のほか、それらを異なるオペレーティング システムや構成用にビルドする方法を開発者が指定できます。 また、異なるファイルに適用できるビルド規則を記述しておき、製品を構成するさまざまなプロジェクトで再利用することにより、一貫したビルド作業を行うことができます。  
  
 以下のセクションでは [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイル形式のいくつかの基本要素について説明します。 基本的なプロジェクト ファイルを作成する方法のチュートリアルについては、[チュートリアル:MSBuild プロジェクト ファイルを最初から作成](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)です。  
  
### <a name="BKMK_Properties"></a> プロパティ  
 プロパティはビルドを設定するためのキーと値のペアです。 プロパティを宣言するには、そのプロパティの名前を持つ要素を [PropertyGroup](../msbuild/propertygroup-element-msbuild.md) 要素の子として作成します。 たとえば、次の コードでは、`BuildDir` という名前のプロパティを作成し、`Build` を値として設定しています。  
  
```  
<PropertyGroup>  
    <BuildDir>Build</BuildDir>  
</PropertyGroup>  
```  
  
 要素内に `Condition` 属性を配置して、プロパティを条件付きで定義することもできます。 条件が `true` と評価されないと、条件付き要素の内容は無視されます。 次の例では、`Configuration` 要素がまだ定義されていない場合に、この要素を定義します。  
  
```  
<Configuration  Condition=" '$(Configuration)' == '' ">Debug</Configuration>  
```  
  
 プロジェクト ファイルでプロパティを参照するには、$(*PropertyName*) という構文を使用します。 たとえば、前の例に示したプロパティを参照するには、`$(BuildDir)` および `$(Configuration)` と記述します。  
  
 プロパティの詳細については、「[MSBuild プロパティ](msbuild-properties1.md)」をご覧ください。  
  
### <a name="BKMK_Items"></a> 項目  
 項目はビルド システムへの入力であり、通常はファイルを表します。 項目はユーザー定義の項目名に基づいて項目の種類にグループ化されます。 これらの項目の種類は、タスクのパラメーターとして使用できます。タスクでは、個々の項目を使用してビルド処理の各ステップを実行します。  
  
 項目は、その項目の種類名を名前に持つ要素を、[ItemGroup](../msbuild/itemgroup-element-msbuild.md) 要素の子として作成することにより、プロジェクト ファイルで宣言します。 たとえば、次のコードでは、`Compile` という名前の項目の種類を作成し、2 つのファイルを含めています。  
  
```  
<ItemGroup>  
    <Compile Include = "file1.cs"/>  
    <Compile Include = "file2.cs"/>  
</ItemGroup>  
```  
  
 プロジェクト ファイルで項目の種類を参照するには、@(*ItemType*) という構文を使用します。 たとえば、この例に示した項目の種類を参照するには、`@(Compile)` と記述します。  
  
 MSBuild では、要素名および属性名では大文字と小文字が区別されますが、 プロパティ名、項目名、メタデータ名では、大文字と小文字は区別されません。 次の例では、`Compile`、`comPile`、または大文字小文字が異なるさらに別の項目の種類のいずれかを作成し、項目の種類に対して "one.cs;two.cs" という値を割り当てます。  
  
```  
<ItemGroup>  
  <Compile Include="one.cs" />  
  <comPile Include="two.cs" />  
</ItemGroup>  
```  
  
 項目はワイルドカード文字を使って宣言できるほか、メタデータを追加することで、より高度なビルド作業を行うことができます。 項目の詳細については、「[項目](../msbuild/msbuild-items.md)」をご覧ください。  
  
### <a name="BKMK_Tasks"></a> タスク  
 タスクとは、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトでビルド処理を実行するために使用される一連の実行可能コードです。 たとえば、タスクでは入力ファイルをコンパイルしたり、外部ツールを実行したりします。 タスクは再利用が可能で、複数の開発者が複数のプロジェクトで共有できます。  
  
 タスクの実行ロジックはマネージド コードで記述され、[UsingTask](../msbuild/usingtask-element-msbuild.md) 要素を使用して [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] にマップされます。 <xref:Microsoft.Build.Framework.ITask> インターフェイスを実装するマネージド型を記述することにより、独自のタスクを作成できます。 タスクを記述する方法の詳細については、「[タスクの作成](../msbuild/task-writing.md)」をご覧ください。  
  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] には、実際の要件に合わせて変更できる一般的なタスクが含まれています。  例は、ファイルをコピーする [Copy](../msbuild/copy-task.md)、ディレクトリを作成する [MakeDir](../msbuild/makedir-task.md)、Visual C# ソース コード ファイルをコンパイルする [Csc](../msbuild/csc-task.md) などです。 使用可能なタスクと使用法については、「[タスク リファレンス](../msbuild/msbuild-task-reference.md)」をご覧ください。  
  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイルでタスクを実行するには、タスク名を名前に持つ要素を [Target](../msbuild/target-element-msbuild.md) 要素の子として作成します。 一般に、タスクは、要素の属性として渡されるパラメーターを受け取ります。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] のプロパティと項目の両方をパラメーターとして使用できます。 たとえば、次のコードでは、[MakeDir](../msbuild/makedir-task.md) タスクを呼び出し、先ほどの例で宣言した `BuildDir` プロパティの値を渡しています。  
  
```  
<Target Name="MakeBuildDirectory">  
    <MakeDir  Directories="$(BuildDir)" />  
</Target>  
```  
  
 タスクの詳細については、「[MSBuild タスク](../msbuild/msbuild-tasks.md)」をご覧ください。  
  
### <a name="BKMK_Targets"></a> ターゲット  
 ターゲットは、タスクを特定の順序でグループ化し、プロジェクト ファイルの各セクションを、ビルド プロセスのエントリ ポイントとして公開する役割を果たします。 読みやすさや拡張性を高める目的で、複数のターゲットを論理的なセクションとしてグループ化することもできます。 ビルド ステップを複数のターゲットに分割することにより、他のターゲットから、一部のビルド処理だけを呼び出すことができ、そのコード セクションをすべてのターゲットに逐一コピーする手間をなくすことができます。 たとえば、ビルド処理の複数のエントリ ポイントで、参照をビルドする必要がある場合、参照をビルドするターゲットを作成しておけば、必要なすべてのエントリ ポイントからそのターゲットを実行できます。  
  
 ターゲットは、プロジェクト ファイル内で、[Target](../msbuild/target-element-msbuild.md) 要素を使用して宣言します。 たとえば、次のコードでは、先ほどの例で宣言した項目のリストをパラメーターに指定して [Csc](../msbuild/csc-task.md) タスクを呼び出す、`Compile` という名前のターゲットを作成しています。  
  
```  
<Target Name="Compile">  
    <Csc Sources="@(Compile)" />  
</Target>  
```  
  
 ターゲットを使用して相互の関係を定義し、依存関係の分析を実行するなど、より高度なシナリオにも対応しています。これにより、ターゲットが最新のものである場合に、ビルド処理からセクション全体をスキップするようなことが可能となります。 ターゲットの詳細については、「[MSBuild ターゲット](../msbuild/msbuild-targets.md)」をご覧ください。  
  
## <a name="BKMK_BuildLogs"></a> ビルド ログ  
 コンソールまたは別の出力デバイスにビルド エラー、警告、およびメッセージを記録できます。 詳細については、「[ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)」と「[MSBuild でのログ](../msbuild/logging-in-msbuild.md)」をご覧ください。  
  
## <a name="BKMK_VisualStudio"></a> Visual Studio での MSBuild の使用  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイル形式を使用して、マネージド プロジェクトに関するビルド情報を保存します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] インターフェイスを使用してプロジェクト設定に追加や変更が加えられると、プロジェクトごとに生成される .*proj ファイルにその内容が反映されます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] のホスト インスタンスを使用して、マネージド プロジェクトをビルドします。 つまり、マネージド プロジェクトは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でも、コマンド プロンプトを使用しても ([!INCLUDE[vsprvs](../includes/vsprvs-md.md)] がインストールされていない場合でも)、同じようにビルドできます。  
  
 Visual Studio で MSBuild を使用する方法のチュートリアルについては、[チュートリアル: MSBuild の使用](../msbuild/walkthrough-using-msbuild.md)に関するページを参照してください。  
  
## <a name="BKMK_Multitargeting"></a> マルチ ターゲット  
 Visual Studio を使用すると、いくつかのバージョンの .NET Framework のうち、任意のバージョンで動作するようにアプリケーションをコンパイルできます。 たとえば、あるアプリケーションを 32 ビット プラットフォーム上の .NET Framework 2.0 で動作するようにコンパイルしたり、これと同じアプリケーションを 64 ビット プラットフォーム上の .NET Framework 4.5 で動作するようにコンパイルしたりできます。 複数のフレームワークに対してコンパイルする機能をマルチ ターゲットといいます。  
  
 マルチ ターゲットには、次のような利点があります。  
  
- バージョン 2.0、3.0、3.5 などの以前のバージョンの .NET Framework を対象とするアプリケーションを開発できます。  
  
- Silverlight など、.NET Framework 以外のフレームワークを対象にできます。  
  
- ターゲット フレームワークの定義済みのサブセットである*フレームワーク プロファイル*を対象にできます。  
  
- 現在のバージョンの .NET Framework 用サービス パックがリリースされた場合、そのバージョンを対象にできます。  
  
- 複数バージョン対応により、アプリケーションが、対象となるフレームワークやプラットフォームのみで利用できる機能を使うことができます。  
  
  詳細については、[MSBuild のマルチ ターゲット](../msbuild/msbuild-multitargeting-overview.md)に関する記事をご覧ください。  
  
## <a name="related-topics"></a>関連トピック  
  
|タイトル|説明|  
|-----------|-----------------|  
|[チュートリアル: 最初から MSBuild プロジェクト ファイルを作成します。](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)|テキスト エディターのみを使用して、基本的なプロジェクト ファイルをインクリメント方式で作成する方法について説明します。|  
|[チュートリアル: MSBuild の使用](../msbuild/walkthrough-using-msbuild.md)|MSBuild のビルド ブロックについて説明し、Visual Studio IDE を閉じずに MSBuild プロジェクトを記述、操作、およびデバッグする方法について説明します。|  
|[MSBuild の概念](../msbuild/msbuild-concepts.md)|MSBuild の 4 つのビルド ブロックであるプロパティ、項目、ターゲット、およびタスクについて説明します。|  
|[項目](../msbuild/msbuild-items.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] ファイル形式の一般的な概念と、各構成要素の組み合わせ方について説明します。|  
|[MSBuild プロパティ](msbuild-properties1.md)|プロパティとプロパティ コレクションについて説明します。 プロパティはビルドを設定するためのキーと値のペアです。|  
|[ターゲット](../msbuild/msbuild-targets.md)|タスクを特定の順序でグループ化し、コマンド ラインからビルド処理のセクションを呼び出すことができるようにする方法について説明します。|  
|[タスク](../msbuild/msbuild-tasks.md)|実行可能コードにおける、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] による分割不可能なビルド処理の実行単位を作成する方法について説明します。|  
|[条件](../msbuild/msbuild-conditions.md)|MSBuild の要素で `Condition` 属性を使用する方法について説明します。|  
|[詳細な概念](../msbuild/msbuild-advanced-concepts.md)|バッチ処理、変換の実行、複数バージョン対応など、高度な利用法を紹介します。|  
|[MSBuild でのログ](../msbuild/logging-in-msbuild.md)|ビルド イベント、メッセージ、およびエラーを記録する方法について説明します。|  
|[その他のリソース](../msbuild/additional-msbuild-resources.md)|MSBuild に関する詳細な情報を提供するコミュニティやサポートのリソースを紹介します。|  
  
## <a name="reference"></a>参照  
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)  
 リファレンス情報を示すトピックへのリンクを提供します。  
  
 用語集  
 MSBuild で共通に使用される用語を定義します。
