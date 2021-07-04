---
title: 参照マネージャーで参照を追加する
description: '[参照マネージャー] ダイアログ ボックスを使用して、開発したコンポーネントに参照を追加し、管理する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 08/02/2019
ms.topic: how-to
helpviewer_keywords:
- C# projects, references
- references [Visual Studio], adding
- assemblies [Visual Studio], references
- Visual Basic projects, references
- project references, adding
- referencing components, adding references
- project references, removing
- referencing assemblies
- referencing components, removing references
- references [Visual Studio], removing
- referencing components, assemblies not listed
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 552ec8364bb58b72199bacecca99283303eb174c
ms.sourcegitcommit: d3658667e768d7516cbf4461ec47bf24c8fcb7e6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112924917"
---
# <a name="how-to-add-or-remove-references-by-using-the-reference-manager"></a>方法: 参照マネージャーを使用して参照を追加または削除する

[参照マネージャー] ダイアログ ボックスを使用し、自分で、あるいは Microsoft か他の会社が開発したコンポーネントに参照を追加し、管理できます。 ユニバーサル Windows アプリを開発している場合、プロジェクトはすべての正しい Windows SDK DLL を自動的に参照します。 .NET アプリケーションを開発している場合、プロジェクトは *mscorlib.dll* を自動的に参照します。 一部の .NET API は、手動で追加する必要があるコンポーネントで公開されます。 COM コンポーネントまたはカスタム コンポーネントへの参照は、手動で追加する必要があります。

## <a name="reference-manager-dialog-box"></a>[参照マネージャー] ダイアログ ボックス

[参照マネージャー] ダイアログ ボックスの左側には、プロジェクト タイプに応じたさまざまなカテゴリが表示されます。

- **アセンブリ** には、**Framework** と **拡張機能** の各サブグループが含まれます。

- **COM** には、参照できるすべての COM コンポーネントの一覧が表示されます。

- **プロジェクト**

- **共有プロジェクト**

- **Windows** には、**コア** と **拡張機能** の各サブグループが含まれます。 **[オブジェクト ブラウザー]** を使って Windows SDK または拡張 SDK 内の参照を探索できます。

- **最近** 使用したサブグループを **参照** します。
 
    > [!NOTE]
    > C++ プロジェクトを開発している場合は、[参照マネージャー] ダイアログ ボックスに **[参照]** が表示されない場合があります。

## <a name="add-a-reference"></a>参照を追加する

1. **ソリューション エクスプローラー** で、 **[参照]** ノードまたは **[依存関係]** ノードを右クリックし、 **[参照の追加]** を選びます。 あるいは、プロジェクト ノードを右クリックし、 **[追加]**  >  **[参照]** の順に選択します。

   **[参照マネージャー]** は、使用可能な参照を開いてグループごとに表示します。

2. 追加する参照を指定した後、 **[OK]** を選びます。

## <a name="assemblies-tab"></a>[アセンブリ] タブ

**[アセンブリ]** タブには、参照に使うことができるすべての .NET アセンブリが一覧表示されます。 グローバル アセンブリ キャッシュ (GAC) 内のアセンブリは実行時環境の一部であるため、 **[アセンブリ]** タブでは GAC からのアセンブリはどれもリスト表示されません。 GAC に登録されているアセンブリへの参照を含むアプリケーションを配置またはコピーした場合は、 **[ローカル コピー]** の設定とはかかわりなく、そのアセンブリがアプリケーションと共に配置またはコピーされることはありません。 詳細については、「[プロジェクト内の参照の管理](../ide/managing-references-in-a-project.md)」を参照してください。

EnvDTE 名前空間 (<xref:EnvDTE>、<xref:EnvDTE80>、<xref:EnvDTE90>、<xref:EnvDTE90a>、または <xref:EnvDTE100>) に手動で参照を追加するときは、 **[プロパティ]** ウィンドウで参照の **[相互運用型の埋め込み]** プロパティを **False** に設定します。 このプロパティを **True** に設定すると、埋め込むことができない EnvDTE プロパティが原因でビルドの問題が発生する可能性があります。

すべてのデスクトップ プロジェクトには、**mscorlib** への暗黙的な参照が含まれます。 Visual Basic プロジェクトには、<xref:Microsoft.VisualBasic> への暗黙的な参照が含まれます。 **System.Core** が参照のリストから削除された場合でも、すべてのプロジェクトに System.Core への暗黙的な参照が含まれます。

プロジェクトの種類がアセンブリをサポートしていない場合は、[参照マネージャー] ダイアログ ボックスの中に [アセンブリ] タブが表示されません。

**[アセンブリ]** タブの中には、次の 2 つのサブタブがあります。

1. **[Framework]** には、対象のフレームワークを形成するすべてのアセンブリが一覧表示されます。

   .NET Core またはユニバーサル Windows プラットフォームを対象にしないプロジェクトの場合、 **[Framework]** タブに対象フレームワークのアセンブリが列挙されます。 ユーザーは、アプリケーションで必要とされる参照を追加する必要があります。

   ユニバーサル Windows プロジェクトには既定で、対象のフレームワーク内にあるすべてのアセンブリへの参照が含まれています。 マネージド プロジェクトでは、**ソリューション エクスプローラー** 内の **[参照]** フォルダーの下にある 1 つの読み取り専用ノードが、フレームワーク全体に対する参照を示します。 したがって、 **[Framework]** タブでは、フレームワークからのどのアセンブリも列挙されず、代わりに次のメッセージが表示されます。"すべての Framework アセンブリが既に参照されています。 オブジェクト ブラウザーを使用して Framework 内の参照を調べてください。"

2. **[拡張機能]** には、対象のフレームワークを拡張するためにコンポーネントおよびコントロールを扱う外部販売元が開発したすべてのアセンブリの一覧が表示されます。 ユーザー アプリケーションの目的によっては、これらのアセンブリが必要になることがあります。

   次の場所に登録されているアセンブリを列挙することによって、**拡張機能** が設定されます。

   32 ビット コンピューター:
   - `HKEY_CURRENT_USER\SOFTWARE\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]`
   - `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]`

   64 ビット コンピューター:
   - `HKEY_CURRENT_USER\SOFTWARE\Wow6432Node\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]`
   - `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]`

   および、[ターゲット フレームワーク識別子] の古いバージョン

   たとえば、プロジェクトが 32 ビット コンピューター上の .NET Framework 4 を対象とする場合は、**拡張機能は** *\Microsoft\.NETFramework\v4.0\AssemblyFoldersEx*、 *\Microsoft\.NETFramework\v3.5\AssemblyFoldersEx*、 *\Microsoft\.NETFramework\v3.0\AssemblyFoldersEx*、 *\Microsoft\.NETFramework\v2.0\AssemblyFoldersEx* の下に登録されているアセンブリを列挙します。

プロジェクトのフレームワーク バージョンによっては、一部のコンポーネントが一覧に表示されないことがあります。 これは、次のような条件で発生します。

- 最新のフレームワーク バージョンを使用するコンポーネントは、旧バージョンを対象とするプロジェクトとは互換性がありません。

   プロジェクトのターゲット フレームワークのバージョンを変更する方法について詳しくは、「[フレームワーク対象設定機能の概要](visual-studio-multi-targeting-overview.md)」をご覧ください。

- .NET Framework 4 を使用するコンポーネントは、.NET Framework 4.5 を対象とするプロジェクトと互換性がありません。

コンパイル エラーが発生する可能性があるため、同じソリューション内の他のプロジェクトの出力に対するファイル参照は追加しないでください。 代わりに、 **[参照の追加]** ダイアログ ボックスの **[プロジェクト]** タブを使ってプロジェクト間参照を作成します。 そうすることによってプロジェクトで作成するクラス ライブラリを管理する機能が向上し、チーム開発が簡単になります。 詳しくは、「[壊れた参照のトラブルシューティング](../ide/troubleshooting-broken-references.md)」をご覧ください。

> [!NOTE]
> Visual Studio 2015 以降では、一方のプロジェクトが対象とするフレームワーク バージョンが .NET Framework 4.5 以降で、他方のプロジェクトが対象とするバージョンが .NET Framework 2、3、3.5、または 4.0 である場合、プロジェクト参照ではなくファイル参照が作成されます。

### <a name="to-display-an-assembly-in-the-add-reference-dialog-box"></a>[参照の追加] ダイアログ ボックスにアセンブリを表示するには

- アセンブリを次の場所のいずれかに移動またはコピーします。

  - 現在のプロジェクト ディレクトリ。 ここにあるアセンブリは、 **[参照]** タブに表示されます。

  - 同じソリューション内のその他のプロジェクト ディレクトリ。 ここにあるアセンブリは、 **[プロジェクト]** タブに表示されます。

  \- または

- 表示するアセンブリの場所を指定するレジストリ キーを設定します。

  32 ビット オペレーティング システムでは、次のいずれかのレジストリ キーを追加します。

  - `[HKEY_CURRENT_USER\SOFTWARE\Microsoft\.NETFramework\<VersionMinimum>\AssemblyFoldersEx\MyAssemblies]@="<AssemblyLocation>"`

  - `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\<VersionMinimum>\AssemblyFoldersEx\MyAssemblies]@="<AssemblyLocation>"`

  64 ビット オペレーティング システムでは、32 ビットのレジストリ ハイブで次のいずれかのレジストリ キーを追加します。

  - `[HKEY_CURRENT_USER\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\<VersionMinimum>\AssemblyFoldersEx\MyAssemblies]@="<AssemblyLocation>"`

  - `[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\<VersionMinimum>\AssemblyFoldersEx\MyAssemblies]@="<AssemblyLocation>"`

  *\<VersionMinimum\>* は、適用されるフレームワークの最小バージョンです。 *\<VersionMinimum\>* が v3.0 の場合、*AssemblyFoldersEx* で指定したフォルダーは、.NET Framework 3.0 以降を対象にしたプロジェクトに適用されます。

  *\<AssemblyLocation\>* は、*C:\MyAssemblies* など、 **[参照の追加]** ダイアログ ボックスに表示されるアセンブリのディレクトリです。

  `HKEY_LOCAL_MACHINE` ノードにレジストリ キーを作成すると、すべてのユーザーが特定の場所にあるアセンブリを **[参照の追加]** ダイアログ ボックスに表示できるようになります。 `HKEY_CURRENT_USER` ノードにレジストリ キーを作成すると、現在のユーザーの設定にのみ影響します。

  **[参照の追加]** ダイアログ ボックスを再度開きます。 アセンブリが **[.NET]** タブに表示されます。表示されない場合は、指定した *AssemblyLocation* ディレクトリにアセンブリが配置されていることを確認し、Visual Studio を再起動して、もう一度実行してみてください。

## <a name="projects-tab"></a>[プロジェクト] タブ

**[プロジェクト]** タブ内の **[ソリューション]** サブタブには、現在のソリューション内に存在し互換性のあるすべてのプロジェクトが表示されます。

プロジェクトは、異なるフレームワーク バージョンを対象とする別のプロジェクトを参照できます。 たとえば、.NET Framework 4 を対象とするプロジェクトを作成し、その中で、.NET Framework 2 を想定してビルドされたアセンブリを参照することができます。 ただし、.NET Framework 2 プロジェクトから、.NET Framework 4 プロジェクトを参照することはできません。 詳細については、[フレームワークのターゲット設定](../ide/visual-studio-multi-targeting-overview.md)に関するページを参照してください。

> [!NOTE]
> .NET Framework 4 を対象にするプロジェクトは、.NET Framework 4 Client Profile を対象とするプロジェクトと互換性がありません。

## <a name="shared-projects-tab"></a>[共有プロジェクト] タブ

[参照マネージャー] ダイアログ ボックスの **[共有プロジェクト]** タブで、共有プロジェクトへの参照を追加します。 [共有プロジェクト](/xamarin/cross-platform/app-fundamentals/shared-projects?tabs=windows) を使用すると、多くのさまざまなアプリケーション プロジェクトによって参照される共通のコードを記述できます。

## <a name="universal-windows-tab"></a>[ユニバーサル Windows] タブ

**[ユニバーサル Windows]** タブには、Windows オペレーティング システムを実行しているプラットフォームに固有であるすべての SDK が一覧表示されます。
このタブには、2 つのサブグループがあります。**コア** と **拡張機能**。

### <a name="core-subgroup"></a>[コア] サブグループ

ユニバーサル Windows アプリ プロジェクトには、既定では、ユニバーサル Windows SDK への参照があります。 したがって、 **[参照マネージャー]** の **[コア]** サブグループでは、ユニバーサル Windows SDK からのアセンブリはいずれも列挙されません。

### <a name="extensions-subgroup"></a>[拡張機能] サブグループ

**[拡張機能]** で、対象の Windows プラットフォームを拡張するユーザー SDK が一覧表示されます。

SDK は、Visual Studio が単一のコンポーネントとして取り扱うファイルのコレクションです。 **[拡張機能]** タブで、[参照マネージャー] ダイアログ ボックスを開いたプロジェクトに対して適用される複数の SDK は単一エントリとして表示されます。 プロジェクトに追加した場合は、SDK のすべての内容が Visual Studio によって使用されます。その結果、IntelliSense、ツールボックス、デザイナー、オブジェクト ブラウザー、ビルド、配置、デバッグ、およびパッケージ化で SDK の内容を活用するために、ユーザーが追加のアクションを実行する必要がなくなります。

**[拡張機能]** タブに SDK を表示する方法については、「[ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)」をご覧ください。

> [!NOTE]
> 別の SDK に依存する SDK がプロジェクトで参照されている場合、2 番目の SDK への参照を手動で追加しない限り、Visual Studio で 2 番目の SDK は使用されません。 ユーザーが **[拡張機能]** タブでいずれかの SDK を選択した場合は、[参照マネージャー] ダイアログ ボックスの詳細ウィンドウに一覧表示された依存関係を確認することで、SDK の依存関係を容易に識別できます。

プロジェクトの種類で [拡張機能] がサポートされていない場合、このタブは、[参照マネージャー] ダイアログ ボックスに表示されません。

## <a name="com-tab"></a>[COM] タブ

**[COM]** タブには、参照できるすべての COM コンポーネントの一覧が表示されます。 内部マニフェストを含む登録済みの COM DLL に参照を追加する場合は、その DLL の登録をまず解除してください。 そうしない場合は、Visual Studio は、アセンブリ参照をネイティブ DLL ではなく、ActiveX コントロールとして追加します。

プロジェクトの種類が COM をサポートしていない場合、[参照マネージャー] ダイアログ ボックスに [COM] タブは表示されません。

## <a name="browse"></a>参照

**[参照]** ボタンを使って、ファイル システム内のコンポーネントを参照できます。

プロジェクトは、異なるフレームワーク バージョンを対象とするコンポーネントを参照できます。 たとえば、.NET Framework 4.7 を対象とするアプリケーションを作成し、そのコンポーネントで .NET Framework 4 を対象とするコンポーネントを参照します。 詳細については、[フレームワークのターゲット設定](../ide/visual-studio-multi-targeting-overview.md)に関するページを参照してください。

同じソリューション内にある別のプロジェクトの出力に対するファイル参照を追加しないでください。そのやり方ではコンパイル エラーが発生する可能性があります。 代わりに、[参照マネージャー] ダイアログ ボックスの **[ソリューション]** タブを使ってプロジェクト間参照を作成します。 そうすることによってプロジェクトで作成するクラス ライブラリを管理する機能が向上し、チーム開発が簡単になります。 詳しくは、「[壊れた参照のトラブルシューティング](../ide/troubleshooting-broken-references.md)」をご覧ください。

SDK を参照してプロジェクトに追加することはできません。 ファイル (たとえば、アセンブリまたは *.winmd*) のみを参照してプロジェクトに追加することができます。

WinMD に対するファイル参照を行う場合に予期されるレイアウトは、 *\<FileName>.winmd*、 *\<FileName>.dll*、および *\<FileName>.pri* というすべてのファイルが並行して配置されることです。 次のシナリオで WinMD を参照する場合は、不完全なファイル セットがプロジェクトの出力ディレクトリにコピーされるため、ビルド エラーとランタイム エラーが発生します。

- **ネイティブ コンポーネント**: ネイティブ プロジェクトは、分離された名前空間ごとに 1 つの WinMD を作成し、実装全体を含む 1 つの DLL を作成します。 各 WinMD は、共通点のない名前になります。 このネイティブ コンポーネント ファイルを参照するときに、MSBuild は、共通点のない名前を付けられた複数の WinMD が 1 つのコンポーネントを形成することを認識しません。 その結果、同じ名前を付けられた *\<FileName>.dll* と *\<FileName>.winmd* のみがコピーされ、ランタイム エラーが発生します。 この問題を回避するには、拡張機能 SDK を作成します。 詳しくは、「[ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)」をご覧ください。

- **コントロールの使用**: 少なくとも XAML コントロールは、 *\<FileName>.winmd*、 *\<FileName>.dll*、 *\<FileName>.pri*、 *\<XamlName>.xaml*、および *\<ImageName>.jpg* によって形成されます。 プロジェクトをビルドするときに、ファイル参照に関連付けられたリソース ファイルはプロジェクトの出力ディレクトリにコピーされず、 *\<FileName>.winmd*、 *\<FileName>.dll*、および *\<FileName>.pri* のみがコピーされます。 リソースの *\<XamlName>.xaml* と *\<ImageName>.jpg* が見つからないことをユーザーに通知するために、ビルド エラーが記録されます。 ビルド、デバッグ、および実行時の動作を成功させるには、ユーザーはプロジェクトの出力ディレクトリにこれらのリソース ファイルを手動でコピーする必要があります。 この問題を回避するには、「[ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)」の手順に従って拡張機能 SDK を作成するか、プロジェクト ファイルを編集して次のプロパティを追加します。

    ```xml
    <PropertyGroup>
       <GenerateLibraryOutput>True</GenerateLibraryOutput>
    </PropertyGroup>
    ```

    > [!NOTE]
    > プロパティを追加した場合は、ビルド速度が遅くなる可能性があります。

## <a name="recent"></a>最近使用したファイル

**[アセンブリ]** 、 **[COM]** 、 **[Windows]** 、 **[参照]** はいずれも **[最近使用したファイル]** タブをサポートし、このタブではプロジェクトに最近追加されたコンポーネントのリストが列挙されます。

## <a name="search"></a>検索

[参照マネージャー] ダイアログ ボックス内の検索バーは、現在フォーカスが置かれているタブを対象として動作します。 たとえば、 **[ソリューション]** タブにフォーカスがあるときにユーザーが検索バーに「System」と入力した場合は、"System" という文字列を含むプロジェクト名がソリューションを形成している状況以外では、検索結果が返されません。

## <a name="see-also"></a>関連項目

- [プロジェクト内の参照の管理](../ide/managing-references-in-a-project.md)
