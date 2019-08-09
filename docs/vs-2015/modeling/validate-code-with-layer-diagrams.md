---
title: レイヤー図を使用したコードの検証 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- layer diagrams, validating
- validation, layer diagrams
- validation, code
- code exploration, validating
- architecture, validating
- Visual Studio Ultimate, validating code
- validation, architecture
- validation, dependencies
- MSBuild, tasks
- MSBuild, layer diagrams
- MSBuild, validating code
ms.assetid: 70cbe55d-4b33-4355-b0a7-88c770a6f75c
caps.latest.revision: 84
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d536a4aaa3c54024a8189a66c2471cb9ae9d4121
ms.sourcegitcommit: b56dc6fadc6c924beed36bb4c2ccc16cf6bcfa1c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2019
ms.locfileid: "68739665"
---
# <a name="validate-code-with-layer-diagrams"></a>レイヤー図を使用したコードの検証
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コードが設計と競合しないことを確認するには、Visual Studio でレイヤー図を使用してコードを検証します。 これが次の点で役立つ場合があります。  
  
- レイヤー図のコードと依存関係で依存関係間の競合を見つける。  
  
- 提案された変更によって影響を受ける可能性がある依存関係を見つける。  
  
   たとえば、レイヤー図を編集して予測されるアーキテクチャの変更を表示した後、コードを検証して、影響を受ける依存関係を確認できます。  
  
- コードを別の設計にリファクターまたは移行する。  
  
   コードを別のアーキテクチャに移動したときに作業が必要なコード、または依存関係を見つけます。  
  
  **必要条件**  
  
- Visual Studio  
  
- Team Foundation ビルド サーバーにインストールされた Visual Studio (Team Foundation ビルドを使用してコードを自動的に検証するために必要)  
  
- レイヤー図を使用するモデリング プロジェクトが含まれたソリューション。 このレイヤー図は、検証する対象の Visual C# プロジェクトまたは Visual Basic .NET プロジェクトの成果物にリンクしている必要があります。 「[コードからレイヤー図を作成する」を](../modeling/create-layer-diagrams-from-your-code.md)参照してください。  
  
  この機能をサポートする Visual Studio のバージョンを確認するには、「 [アーキテクチャ ツールとモデリング ツールのバージョン サポート](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。  
  
  Visual Studio で開いているレイヤー図から、またはコマンド プロンプトから、コードを手動で検証できます。 ローカル ビルドまたは Team Foundation ビルドの実行時に、コードを自動的に検証することもできます。 Channel [9 のビデオを参照してください。レイヤー図](http://go.microsoft.com/fwlink/?LinkID=252073)を使用して、アーキテクチャの設計と検証を行います。  
  
> [!IMPORTANT]
> Team Foundation ビルドを使用してレイヤー検証を実行する場合は、ビルド サーバーに同じバージョンの Visual Studio をインストールすることも必要です。  
  
- [項目が検証をサポートしているかどうかを確認する](#SupportsValidation)  
  
- [検証用の他の .NET アセンブリおよびプロジェクトを含める](#IncludeReferences)  
  
- [手動によるコードの検証](#ValidateManually)  
  
- [コードを自動的に検証する](#ValidateAuto)  
  
- [レイヤー検証に関する問題のトラブルシューティング](#TroubleshootingValidation)  
  
- [レイヤー検証エラーの理解と解決](#UnderstandingValidationErrors)  
  
## <a name="SupportsValidation"></a>項目が検証をサポートしているかどうかを確認する  
 複数のアプリ間で共有される Web サイト、Office ドキュメント、プレーン テキスト ファイル、プロジェクトのファイルにレイヤーをリンクできますが、そのレイヤーは検証プロセスは含まれません。 個々のレイヤー間に依存関係が表示されない場合、これらのレイヤーにリンクされているプロジェクトやアセンブリへの参照については、検証エラーは表示されません。 このような参照は、コードがこれらの参照を使用している場合を除き、依存関係と見なされません。  
  
1. レイヤー図で1つまたは複数のレイヤーを選択し、選択した内容を右クリックして、[**リンクの表示**] をクリックします。  
  
2. **レイヤーエクスプローラー**で、[検証の**サポート**] 列を確認します。 値が false の場合、この項目では検証がサポートされません。  
  
## <a name="IncludeReferences"></a>検証用の他の .NET アセンブリおよびプロジェクトを含める  
 レイヤー図に項目をドラッグすると、対応する .NET アセンブリまたはプロジェクトへの参照が、モデリングプロジェクトの [**レイヤー参照**] フォルダーに自動的に追加されます。 このフォルダーには、検証時に分析されたアセンブリおよびプロジェクトへの参照が格納されます。 また、その他の検証対象の .NET アセンブリおよびプロジェクトを、手動でレイヤー図にドラッグせずに含めることもできます。  
  
1. **ソリューションエクスプローラー**で、モデリングプロジェクトまたは [**レイヤー参照**] フォルダーを右クリックし、[**参照の追加**] をクリックします。  
  
2. [**参照の追加**] ダイアログボックスで、アセンブリまたはプロジェクトを選択し、[ **OK**] をクリックします。  
  
## <a name="ValidateManually"></a>手動によるコードの検証  
 ソリューション項目にリンクされているレイヤー図が開いている場合は、ダイアグラムから [ショートカットの**検証**] コマンドを実行できます。 コマンドプロンプトを使用して、 **/p: ValidateArchitecture**カスタムプロパティを**True**に設定して**msbuild**コマンドを実行することもできます。 たとえば、コードの変更を行う場合、依存関係の競合を早期にキャッチできるようにレイヤー検証を定期的に実行します。  
  
#### <a name="to-validate-code-from-an-open-layer-diagram"></a>開かれているレイヤー図からコードを検証するには  
  
1. ダイアグラム画面を右クリックし、[アーキテクチャの**検証**] をクリックします。  
  
    > [!NOTE]
    > 既定では、図が検証プロセスに含まれるように、レイヤー図 (レイヤ図) ファイルの "**ビルドアクション**" プロパティが [**検証**] に設定されています。  
  
     **エラー一覧**ウィンドウには、発生したすべてのエラーが報告されます。 検証エラーの詳細については、「[レイヤー検証エラーの理解と解決](#UnderstandingValidationErrors)」を参照してください。  
  
2. 各エラーのソースを表示するには、[**エラー一覧**] ウィンドウでエラーをダブルクリックします。  
  
    > [!NOTE]
    > [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] では、エラーのソースの代わりにコード マップが表示されることがあります。 これは、レイヤー図で指定されていないアセンブリ上にコードの依存関係があるか、レイヤー図で指定された依存関係がコードにない場合に起こります。 コード マップまたはコードをレビューし、依存関係が必要であるかどうかを検証してください。 コードマップの詳細については、「[ソリューション間の依存関係のマッピング](../modeling/map-dependencies-across-your-solutions.md)」を参照してください。  
  
3. エラーを管理するには、「[検証エラーの管理](#ManageErrors)」を参照してください。  
  
#### <a name="to-validate-code-at-the-command-prompt"></a>コマンド プロンプトでコードを検証するには  
  
1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のコマンド プロンプトを開きます。  
  
2. 次のいずれかを選択します。  
  
   - ソリューションの特定のモデリング プロジェクトに対してコードを検証するには、次のカスタム プロパティを使用して [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] を実行します。  
  
     ```  
     msbuild <FilePath+ModelProjectFileName>.modelproj /p:ValidateArchitecture=true  
     ```  
  
     - または  
  
       モデリング プロジェクト (.modelproj) ファイルとレイヤー図が入っているフォルダーを参照し、次のカスタム プロパティを使用して [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] を実行します。  
  
     ```  
     msbuild /p:ValidateArchitecture=true   
     ```  
  
   - ソリューションのすべてのモデリング プロジェクトに対してコードを検証するには、次のカスタム プロパティを使用して [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] を実行します。  
  
     ```  
     msbuild <FilePath+SolutionName>.sln /p:ValidateArchitecture=true   
     ```  
  
     - または  
  
       レイヤー図が入っているモデリング プロジェクトを必ず含むソリューション フォルダーを参照し、次のカスタム プロパティを使用して [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] を実行します。  
  
     ```  
     msbuild /p:ValidateArchitecture=true  
     ```  
  
     発生したすべてのエラーが表示されます。 の詳細[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]については、「 [msbuild](../msbuild/msbuild.md)と[msbuild タスク](../msbuild/msbuild-task.md)」を参照してください。  
  
   検証エラーの詳細については、「[レイヤー検証エラーの理解と解決](#UnderstandingValidationErrors)」を参照してください。  
  
### <a name="ManageErrors"></a>検証エラーの管理  
 開発プロセスの実行中は、検証時に報告される一部の競合を抑制できます。 たとえば、既に解決したエラーや特定のシナリオに関連しないエラーを抑制できます。 エラーを抑制した場合は、[!INCLUDE[esprfound](../includes/esprfound-md.md)] で作業項目をログに記録することをお勧めします。  
  
> [!WARNING]
> 作業項目を作成またはそれにリンクするには、既に TFS ソース コード管理 (SCC) に接続されている必要があります。 別の TFS SCC への接続を開こうとすると、Visual Studio が現在のソリューションを自動的に閉じます。 作業項目を作成またはそれにリンクしようとする前に、適切な SCC に接続されていることを確認してください。 Visual Studio の今後のリリースでは、SCC に接続されていないとメニュー コマンドを使用できません。  
  
##### <a name="to-create-a-work-item-for-a-validation-error"></a>検証エラーの作業項目を作成するには  
  
- [**エラー一覧**] ウィンドウで、エラーを右クリックし、[**作業項目の作成**] をポイントして、作成する作業項目の種類をクリックします。  
  
  [**エラー一覧**] ウィンドウで検証エラーを管理するには、次のタスクを使用します。  
  
|**To**|**次の手順に従います。**|  
|------------|----------------------------|  
|検証中に選択したエラーを抑制する|選択した1つまたは複数のエラーを右クリックし、[**検証エラーの管理**] をポイントして、[**エラーの抑制**] をクリックします。<br /><br /> 抑制されたエラーは、取り消し線付きで表示されます。 次回検証を実行したとき、これらのエラーは表示されません。<br /><br /> 抑制されたエラーは、対応するレイヤー図ファイルの .suppressions ファイルで追跡されます。|  
|選択したエラーの抑制を停止する|選択した抑制されたエラーを右クリックして、[**検証エラーの管理**] をポイントし、[**エラーの抑制を停止**する] をクリックします。<br /><br /> 次回検証を実行したとき、抑制されたエラーのうち選択したものが表示されます。|  
|[**エラー一覧**] ウィンドウで抑制されたエラーをすべて復元します。|[**エラー一覧**] ウィンドウの任意の場所を右クリックし、[**検証エラーの管理**] をポイントし、[抑制された**エラーをすべて表示**] をクリックします。|  
|[**エラー一覧**] ウィンドウで抑制されたエラーをすべて非表示にする|**エラー一覧**ウィンドウ内の任意の場所を右クリックし、[**検証エラーの管理**] をポイントし、[抑制された**エラーをすべて非表示**にする] をクリックします。|  
  
## <a name="ValidateAuto"></a>コードを自動的に検証する  
 ローカル ビルドを実行するたびにレイヤー検証を実行できます。 チームで Team Foundation ビルドを使用する場合、ゲート チェックインを使用してレイヤー検証を実行できます。これは、カスタム MSBuild タスクを作成することで指定できます。また、ビルド レポートを使用して検証エラーを収集することもできます。 ゲートチェックインビルドを作成するには、「[ゲートチェックインビルドプロセスを使用して変更を検証](https://msdn.microsoft.com/library/9cfc8b9c-1023-40fd-8ab5-1b1bd9c172ec)する」を参照してください。  
  
#### <a name="to-validate-code-automatically-during-a-local-build"></a>ローカル ビルド時にコードを自動的に検証するには  
  
- テキスト エディターを使用してモデリング プロジェクト (.modelproj) ファイルを開き、次のプロパティを追加します。  
  
```  
<ValidateArchitecture>true</ValidateArchitecture>  
```  
  
 \- または -  
  
1. **ソリューションエクスプローラー**で、レイヤー図または図を含むモデリングプロジェクトを右クリックし、[**プロパティ**] をクリックします。  
  
2. [**プロパティ**] ウィンドウで、モデリングプロジェクトの [**アーキテクチャの検証**] プロパティを [ **True**] に設定します。  
  
    これには、検証プロセス内のモデリング プロジェクトが含まれます。  
  
3. **ソリューションエクスプローラー**で、検証に使用するレイヤー図 (レイヤ図) ファイルをクリックします。  
  
4. [**プロパティ**] ウィンドウで、ダイアグラムの [**ビルドアクション**] プロパティが [**検証**] に設定されていることを確認します。  
  
    これには、検証プロセス内のレイヤー図が含まれます。  
  
   [エラー一覧] ウィンドウでエラーを管理するには、「[検証エラーの管理](#ManageErrors)」を参照してください。  
  
#### <a name="to-validate-code-automatically-during-a-team-foundation-build"></a>Team Foundation ビルド時にコードを自動的に検証するには  
  
1. **チームエクスプローラー**で、ビルド定義をダブルクリックし、[**処理**] をクリックします。  
  
2. [**ビルドプロセスパラメーター**] の [**コンパイル**] を展開し、[ **MSBuild 引数**] パラメーターに次のように入力します。  
  
    `/p:ValidateArchitecture=true`  
  
   検証エラーの詳細については、「[レイヤー検証エラーの理解と解決](#UnderstandingValidationErrors)」を参照してください。 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] の詳細については、以下のトピックを参照してください。  
  
- [アプリケーションのビルド](/azure/devops/pipelines/index)  
  
- [ビルドプロセスに既定のテンプレートを使用する](https://msdn.microsoft.com/library/43930b12-c21b-4599-a980-2995e3d16e31)  
  
- [UpgradeTemplate .xaml に基づくレガシビルドを変更する](https://msdn.microsoft.com/library/ee1a8259-1dd1-4a10-9563-66c5446ef41c)  
  
- [ビルド プロセス テンプレートのカスタマイズ](https://msdn.microsoft.com/library/b94c58f2-ae6f-4245-bedb-82cd114f6039)  
  
- [実行中のビルドの進行状況を監視する](https://msdn.microsoft.com/library/e51e3bad-2d1d-4b7b-bfcc-c43439c6c8ef)  
  
## <a name="TroubleshootingValidation"></a>レイヤー検証に関する問題のトラブルシューティング  
 レイヤー検証に関する問題とその解決方法について、次の表で説明します。 これらの問題は、コードと設計の間の競合によって発生するエラーとは異なります。 これらのエラーの詳細については、「[レイヤー検証エラーの理解と解決](#UnderstandingValidationErrors)」を参照してください。  
  
|**問題点**|**考えられる原因**|**解決策**|  
|---------------|------------------------|--------------------|  
|検証エラーが予期したとおりに発生しない。|検証はソリューション エクスプローラーの他のレイヤー図からコピーされたレイヤー図および同じモデリング プロジェクトのレイヤー図には機能しません。 この方法でコピーされたレイヤー図には、コピー元のレイヤー図と同じ参照が含まれます。|新しいレイヤー図をモデリング プロジェクトに追加します。<br /><br /> コピー元のレイヤー図から新しいレイヤー図へ要素をコピーします。|  
  
## <a name="UnderstandingValidationErrors"></a>レイヤー検証エラーの理解と解決  
 レイヤー図と照らし合わせてコードを検証すると、コードが設計と競合している場合に検証エラーが発生します。 たとえば、次の条件のとき、検証エラーが発生する場合があります。  
  
- 成果物が不適切なレイヤーに割り当てられている。 この場合、成果物を移動します。  
  
- クラスなどの成果物が、アーキテクチャに違反する形で別のクラスを使用している。 この場合、コードをリファクタリングして依存関係を削除します。  
  
  これらのエラーを解決するには、コードを更新して、検証時にエラーが表示されなくなるようにします。 この作業は、反復的な方法で実行します。  
  
  次のセクションでは、これらのエラーで使用される構文を示し、これらのエラーの意味を説明し、エラーを解決または管理するために実行できることを提示します。  
  
|**構文**|**説明**|  
|----------------|---------------------|  
|*Artifactn*(*Artifacttypen*)|*Artifactn*は、レイヤー図のレイヤーに関連付けられている成果物です。<br /><br /> *Artifacttypen*は、**クラス**や**メソッド**など、 *artifactn*の種類です。たとえば、次のようになります。<br /><br /> MySolution.MyProject.MyClass.MyMethod(Method)|  
|*NamespaceNameN*|名前空間の名前。|  
|*LayerNameN*|レイヤー図のレイヤーの名前。|  
|*DependencyType*|*Artifact1*と*Artifact2*の間の依存関係の種類。 たとえば、 *Artifact1*には*Artifact2*との**呼び出し**関係があります。|  
  
|**エラー構文**|**エラーの説明**|  
|----------------------|---------------------------|  
|AV0001無効な依存関係:*Artifact1*(*ArtifactType1*)--> *Artifact2*(*ArtifactType2*)<br /><br /> レイヤー*LayerName1*、 *LayerName2* &#124;の依存関係:*DependencyType*|*LayerName1* が*LayerName2*に直接依存していないため、 *LayerName1*の*Artifact1*は*LayerName2*の*Artifact2*に依存していてはなりません。|  
|AV1001無効な名前空間:*アー*<br /><br /> レイヤー$ *Ername*&#124;必要な名前空間:*NamespaceName1*&#124;現在の名前空間:*NamespaceName2*|$ *Ername*は、関連付けられた成果物が*NamespaceName1*に属している必要があります。 *アーティファクト*は、 *NamespaceName1*ではなく、 *NamespaceName2*にあります。|  
|AV1002禁止された名前空間に依存:*Artifact1*(*ArtifactType1*)&#124; *Artifact2*(*ArtifactType2*)<br /><br /> レイヤー$ *Ername*&#124;禁止された名前空間:*NamespaceName*&#124;依存関係:*DependencyType*|$ *Ername*は、関連付けられている成果物が*NamespaceName*に依存していないことが必要です。 *Artifact2*が*NamespaceName*にあるため、 *Artifact1*を*Artifact2*に依存させることはできません。|  
|AV1003禁止された名前空間:*成果物*(*Artifacttype*)<br /><br /> レイヤー$ *Ername*&#124;禁止された名前空間:*NamespaceName*|$ *Ername*は、関連付けられた成果物が*NamespaceName*に属することができません。 *成果物*は*NamespaceName*に属します。|  
|AV3001見つからないリンク:'*成果物*' へのレイヤー ' レイヤ*ername*' リンクが見つかりません。 アセンブリ参照が存在することを確認してください。|成果物への *LayerName* リンクが見つかりません。 たとえば、モデリング プロジェクトでクラスを含むアセンブリへの参照が欠落しているために、クラスへのリンクが欠落している場合があります。|  
|AV9001:アーキテクチャ分析で内部エラーが見つかりました。 結果が不完全である可能性があります。 詳細については、ビルド イベント ログの詳細または出力ウィンドウを参照してください。|詳細については、ビルド イベント ログまたは出力ウィンドウを参照してください。|  
  
## <a name="security"></a>セキュリティ  
  
## <a name="see-also"></a>関連項目  
 [開発時のシステムの検証](../modeling/validate-your-system-during-development.md)
