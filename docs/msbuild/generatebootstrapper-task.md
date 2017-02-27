---
title: "GenerateBootstrapper タスク | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-sdk"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/developer/msbuild/2003#GenerateBootstrapper"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "MSBuild GenerateBootstrapper タスク"
  - "GenerateBootstrapper タスク [MSBuild]"
ms.assetid: ca3ba2c6-d2ea-41f2-b7e3-0fc2b0730460
caps.latest.revision: 13
author: "kempb"
ms.author: "kempb"
manager: "ghogen"
caps.handback.revision: 13
---
# <a name="generatebootstrapper-task"></a>GenerateBootstrapper タスク
アプリケーションとその前提条件を検出、ダウンロード、インストールする自動化方法を提供します。 これは、アプリケーションを構成するすべてのコンポーネントの別々のインストーラーを統合する単一のインストーラーとして機能します。  
  
## <a name="task-parameters"></a>タスク パラメーター  
 `GenerateBootstrapper` タスクのパラメーターの説明を次の表に示します。  
  
-   `ApplicationFile`  
  
     省略可能な `String` 型のパラメーターです。  
  
     すべての前提条件がインストールされた後に、アプリケーションのインストールを開始するためにブートストラップが使用するファイルを指定します。 `BootstrapperItems` パラメーターも `ApplicationFile` パラメーターも指定されていない場合、ビルド エラーが発生します。  
  
-   `ApplicationName`  
  
     省略可能な `String` 型のパラメーターです。  
  
     ブートストラップがインストールするアプリケーションの名前を指定します。 この名前は、ブートストラップがインストール中に使用する UI の中で表示されます。  
  
-   `ApplicationRequiresElevation`  
  
     省略可能な `Boolean` 型のパラメーターです。  
  
     `true` である場合、コンポーネントはターゲット コンピューターにインストールされるとき、管理者特権のアクセス許可で実行されます。  
  
-   `ApplicationUrl`  
  
     省略可能な `String` 型のパラメーターです。  
  
     アプリケーションのインストーラーをホストする Web 上の場所を指定します。  
  
-   `BootstrapperComponentFiles`  
  
     省略可能な `String[]` 型の出力パラメーターです。  
  
     ブートストラップ パッケージ ファイルがビルドされた場所を指定します。  
  
-   `BootstrapperItems`  
  
     省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。  
  
     ブートストラップに組み込む製品を指定します。 このパラメーターに渡される項目は、以下の構文に従わなければなりません。  
  
    ```xml  
    <BootstrapperItem  
        Include="ProductCode">  
        <ProductName>  
            ProductName  
        </ProductName>  
    </BootstrapperItem>  
    ```  
  
     `Include` 属性は、インストールすべき前提条件の名前を表すために使用されます。 `ProductName` 項目メタデータは省略可能であり、パッケージが見つからなかった場合にユーザー フレンドリーな名前としてビルド エンジンによって使用されます。 これらの項目は、`ApplicationFile` が指定されている場合を除き、必須の [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 入力パラメーターではありません。 アプリケーション用にインストールすべき前提条件ごとに&1; つの項目を含める必要があります。  
  
     `BootstrapperItems` パラメーターも `ApplicationFile` パラメーターも指定されていない場合、ビルド エラーが発生します。  
  
-   `BootstrapperKeyFile`  
  
     省略可能な `String` 型の出力パラメーターです。  
  
     setup.exe がビルドされた場所を指定します。  
  
-   `ComponentsLocation`  
  
     省略可能な `String` 型のパラメーターです。  
  
     インストールするインストール前提条件をブートストラップが探す場所を指定します。 このパラメーターには、次の値を指定できます。  
  
    -   `HomeSite`: 前提条件がコンポーネント ベンダーによってホストされていることを示します。  
  
    -   `Relative`: 前提条件がアプリケーションと同じ場所にあることを示します。  
  
    -   `Absolute`: 一元化された URL にすべてのコンポーネントがあることを示します。 この値は `ComponentsUrl` 入力パラメーターと共に使用する必要があります。  
  
     `ComponentsLocation` が指定されていない場合は、`HomeSite` が既定で使用されます。  
  
-   `ComponentsUrl`  
  
     省略可能な `String` 型のパラメーターです。  
  
     インストールの前提条件が含まれる URL を指定します。  
  
-   `CopyComponents`  
  
     省略可能な `Boolean` 型のパラメーターです。  
  
     `true` である場合、ブートストラップはすべての出力ファイルを `OutputPath` パラメーターで指定されているパスにコピーします。 `BootstrapperComponentFiles` パラメーターの値はすべてこのパスに基づいたものにしなければなりません。 `false` である場合、ファイルはコピーされず、`BootstrapperComponentFiles` の値は `Path` パラメーターの値に基づいたものとなります。  このパラメーターの既定値は、`true` です。  
  
-   `Culture`  
  
     省略可能な `String` 型のパラメーターです。  
  
     ブートストラップ UI およびインストールの前提条件に使用されるカルチャを指定します。 指定したカルチャが使用不可能である場合、タスクは `FallbackCulture` パラメーターの値を使用します。  
  
-   `FallbackCulture`  
  
     省略可能な `String` 型のパラメーターです。  
  
     ブートストラップ UI およびインストール前提条件に使用する&2; 次カルチャを指定します。  
  
-   `OutputPath`  
  
     省略可能な `String` 型のパラメーターです。  
  
     setup.exe とすべてのパッケージ ファイルのコピー先を指定します。  
  
-   `Path`  
  
     省略可能な `String` 型のパラメーターです。  
  
     使用可能なすべての前提条件パッケージの場所を指定します。  
  
-   `SupportUrl`  
  
     省略可能な `String` 型のパラメーターです。  
  
     ブートストラップのインストールが失敗した場合に提供する URL を指定します。  
  
-   `Validate`  
  
     省略可能な `Boolean` 型のパラメーターです。  
  
     `true` の場合、ブートストラップは指定された入力ブートストラップ項目に対して XSD 検証を実行します。 このパラメーターの既定値は、`false` です。  
  
## <a name="remarks"></a>コメント  
 このタスクでは、上記のパラメーター以外に、<xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承し、このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加パラメーター一覧とそれらの説明については、「[TaskExtension Base Class (TaskExtension 基底クラス)](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、前提条件として [!INCLUDE[dnprdnlong](../code-quality/includes/dnprdnlong_md.md)] がインストールされていなければならないアプリケーションをインストールするために `GenerateBootstrapper` タスクが使用されています。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <BootstrapperFile Include="Microsoft.Net.Framework.2.0">  
            <ProductName>Microsoft .NET Framework 2.0</ProductName>  
        </BootstrapperFile>  
    </ItemGroup>  
  
    <Target Name="BuildBootstrapper">  
        <GenerateBootstrapper  
            ApplicationFile="WindowsApplication1.application"  
            ApplicationName="WindowsApplication1"  
            ApplicationUrl="http://mycomputer"  
            BootstrapperItems="@(BootstrapperFile)"  
            OutputPath="C:\output" />  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>関連項目  
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)


<!--HONumber=Feb17_HO4-->


