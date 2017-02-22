---
title: "ブートストラップ パッケージの作成 | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-deployment"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "FSharp"
  - "VB"
  - "CSharp"
  - "C++"
helpviewer_keywords: 
  - "カスタムの必須コンポーネント"
  - "配置 (アプリケーションを) [Visual Studio], カスタムの必須コンポーネント"
  - "配置 (アプリケーションを) [Visual Studio], 必要条件"
  - "必要条件, カスタム"
  - "RedistList ファイル"
  - "再頒布可能パッケージのリスト"
ms.assetid: ba1a785b-693d-446b-bcae-b88cadee73d1
caps.latest.revision: 45
caps.handback.revision: 45
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# ブートストラップ パッケージの作成
[!INCLUDE[vs2017banner](../code-quality/includes/vs2017banner.md)]

セットアップ プログラムは、Windows インストーラー \(.msi\) ファイルや実行可能プログラムなどの再頒布可能コンポーネントを検出およびインストールするように構成できる汎用的なインストーラーです。 インストーラーはブートストラップとも呼ばれます。 ブートストラップは、コンポーネントのインストールを管理するためのメタデータを指定する、一連の XML マニフェストによってプログラミングされます。  
  
 ブートストラップでは、まず、既にインストールされている必須コンポーネントがあるかどうかが検出されます。 必須コンポーネントがインストールされていない場合、ライセンス条項が表示されます。 次に、エンド ユーザーがライセンス条項に同意すると、必須コンポーネントのインストールが開始されます。 すべての必須コンポーネントが検出された場合は、そのままアプリケーション インストーラーが開始されます。  
  
## カスタム パッケージの作成  
 Visual Studio の XML エディターを使用してマニフェストを生成することができます。 詳細については、[方法: パッケージ マニフェストを作成する](../deployment/how-to-create-a-package-manifest.md) および [方法: 製品マニフェストを作成する](../deployment/how-to-create-a-product-manifest.md) を参照してください。 ブートストラップ パッケージを作成する例については、「[チュートリアル: プライバシー プロンプトを表示するためのカスタム ブートストラップの作成](../deployment/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt.md)」をご覧ください。  
  
 ブートストラップ パッケージを作成するには、Bootstrapper Manifest Generator に EXE 形式または MSI 形式の再頒布可能ファイルを指定する必要があります。 Bootstrapper Manifest Generator によって次のファイルが作成されます。  
  
-   パッケージの言語的に中立なメタデータをすべて含む製品マニフェスト \(product.xml\)。 再頒布可能コンポーネントのすべてのローカライズ バージョンに共通するメタデータが含まれます。  
  
-   言語固有のメタデータを含むパッケージ マニフェスト \(package.xml\)。通常、ローカライズされたエラー メッセージが含まれます。 コンポーネントの各ローカライズ バージョンに対して、少なくとも 1 つのパッケージ マニフェストが必要です。  
  
 これらのファイルが作成されたら、製品マニフェスト ファイルをカスタム ブートストラップ名のフォルダーに格納します。 パッケージ マニフェスト ファイルは、ロケール名のフォルダーに格納します。 たとえば、英語の再頒布用のパッケージ マニフェスト ファイルは、en というフォルダーに格納します。 日本語用は ja、ドイツ語用は de など、ロケールごとにこの手順を繰り返します。 最終的に、カスタム ブートストラップ パッケージは次のようなフォルダー構造になります。  
  
 `CustomBootstrapperPackage`  
  
 `product.xml`  
  
 `CustomBootstrapper.msi`  
  
 `de`  
  
 `eula.rtf`  
  
 `package.xml`  
  
 `en`  
  
 `eula.rtf`  
  
 `package.xml`  
  
 `ja`  
  
 `eula.rtf`  
  
 `package.xml`  
  
 最後に、再頒布可能ファイルをブートストラップ フォルダーにコピーします。 詳細については、「[方法: ローカライズされたブートストラップ パッケージを作成する](../deployment/how-to-create-a-localized-bootstrapper-package.md)」を参照してください。  
  
```  
\Program Files\Microsoft Visual Studio 14.0\SDK\Bootstrapper\Packages  
```  
  
 、または  
  
```  
\Program Files (x86)\Microsoft Visual Studio 14.0\SDK\Bootstrapper\Packages  
```  
  
 ブートストラップ フォルダーの場所は、次のレジストリ キーの **Path** 値からも特定できます。  
  
```  
HKLM\Software\Microsoft\GenericBootstrapper\11.0  
```  
  
 64 ビット システムでは、次のレジストリ キーを使用します。  
  
```  
HKLM\Software\Wow6432Node\Microsoft\GenericBootstrapper\11.0  
```  
  
 再頒布可能コンポーネントは、パッケージのディレクトリの下の専用のサブフォルダーにそれぞれ表示されます。 製品マニフェスト ファイルと再頒布可能ファイルは、このサブフォルダーに格納されます。 コンポーネントのローカライズ バージョンとパッケージ マニフェストは、カルチャ名に従って名前が付けられたサブフォルダーに格納されます。  
  
 これらのファイルをブートストラップ フォルダーにコピーすると、Visual Studio の \[必須コンポーネント\] ダイアログ ボックスにブートストラップ パッケージが自動的に表示されます。 カスタム ブートストラップ パッケージが表示されない場合は、\[必須コンポーネント\] ダイアログ ボックスを閉じてから開き直してください。 詳細については、「[\[必須コンポーネント\] ダイアログ ボックス](../Topic/Prerequisites%20Dialog%20Box.md)」を参照してください。  
  
 ブートストラップによって自動的に設定されるプロパティを次の表に示します。  
  
|プロパティ|説明|  
|-----------|--------|  
|ApplicationName|アプリケーションの名前。|  
|ProcessorArchitecture|実行可能ファイルが対象とするプラットフォームのプロセッサと、ワードあたりのビット数。 次の値があります。<br /><br /> -   Intel<br />-   IA64<br />-   AMD64|  
|[Version9x](https://msdn.microsoft.com/en-us/library/aa372490\(v=vs.140\).aspx)|Microsoft Windows 95、Windows 98、または Windows ME の各オペレーティング システムのバージョン番号。 バージョンの構文は、Major.Minor.ServicePack です。|  
|[VersionNT](https://msdn.microsoft.com/en-us/library/aa372495\(v=vs.140\).xaspx)|Windows NT、Windows 2000、Windows XP、Windows Vista、Windows Server 2008、または Windows 7 の各オペレーティング システムのバージョン番号。 バージョンの構文は、Major.Minor.ServicePack です。|  
|[VersionMSI](https://msdn.microsoft.com/en-us/library/aa372493\(v=vs.140\).aspx)|インストール中に実行される Windows インストーラーのアセンブリ \(msi.dll\) のバージョン。|  
|[AdminUser](https://msdn.microsoft.com/en-us/library/aa367545\(v=vs.140\).aspx)|このプロパティは、ユーザーに管理者特権がある場合に設定されます。 値は true または false です。|  
|InstallMode|インストール モードは、コンポーネントのインストール元の場所を示します。 次の値があります。<br /><br /> -   HomeSite \- ベンダーの Web サイトから必須コンポーネントをインストールします。<br />-   SpecificSite \- 選択した場所から必須コンポーネントをインストールします。<br />-   SameSite \- アプリケーションと同じ場所から必須コンポーネントをインストールします。|  
  
## 再配布可能コンポーネントとアプリケーションのインストールの分離  
 再配布可能ファイルは、セットアップ プロジェクトで配置されないようにすることができます。 そのためには、.NET Framework ディレクトリの RedistList フォルダーに再頒布可能リストを作成します。  
  
 `%ProgramFiles%\Microsoft.NET\RedistList`  
  
 再頒布可能リストは XML ファイルです。このファイルには、*Company Name*.*Component Name*.RedistList.xml という形式の名前を付けます。 たとえば、Acme 社製の Datawidgets というコンポーネントの場合は、Acme.DataWidgets.RedistList.xml にします。 再頒布可能リストの内容は、たとえば次のようになります。  
  
```  
<?xml version="1.0" encoding="UTF-8"?> <FileList Redist="Acme.DataWidgets" > <File AssemblyName="Acme.DataGrid" Version="1.0.0.0" PublicKeyToken="b03f5f7f11d50a3a" Culture="neutral" ProcessorArchitecture="MSIL" InGAC="true" /> </FileList>  
```  
  
## 参照  
 [方法 : ClickOnce アプリケーションと共に必須コンポーネントをインストールする](../Topic/How%20to:%20Install%20Prerequisites%20with%20a%20ClickOnce%20Application.md)   
 [\[必須コンポーネント\] ダイアログ ボックス](../Topic/Prerequisites%20Dialog%20Box.md)   
 [製品およびパッケージ スキーマ リファレンス](../deployment/product-and-package-schema-reference.md)   
 [Visual Studio 2005 ブートストラップを使用してインストールを促進する](http://go.microsoft.com/fwlink/?LinkId=107537)