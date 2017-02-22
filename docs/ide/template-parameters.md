---
title: "テンプレート名 | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "項目テンプレート, パラメーター"
  - "プロジェクト テンプレート, パラメーター"
  - "テンプレート パラメーター [Visual Studio]"
  - "Visual Studio のテンプレート, パラメーター"
ms.assetid: 1b567143-08c6-4d7a-b484-49f0671754fe
caps.latest.revision: 24
caps.handback.revision: 24
author: "kempb"
ms.author: "kempb"
manager: "ghogen"
---
# テンプレート名
[!INCLUDE[vs2017banner](../code-quality/includes/vs2017banner.md)]

テンプレート内でパラメーターを使用すると、テンプレートがインスタンス化されたときに、テンプレート内の主要な部分 \(クラス名や名前空間など\) の値を置き換えることができます。  **\[新しいプロジェクト\]** ダイアログ ボックスまたは **\[新しい項目の追加\]** ダイアログ ボックスで **\[OK\]** をクリックすると、これらのパラメーターが、バックグラウンドで実行されているテンプレート ウィザードによって置き換えられます。  
  
## テンプレート パラメーターの宣言と有効化  
 テンプレート パラメーターは、$*parameter* という形式で宣言します。  次のように記述します。  
  
-   $safeprojectname$  
  
-   $guid1$  
  
-   $guid5$  
  
#### テンプレートでパラメーター置換を有効にするには  
  
1.  テンプレートの .vstemplate ファイル内で、パラメーター置換を有効にする項目に対応する `ProjectItem` 要素を見つけます。  
  
2.  `ProjectItem` 要素の `ReplaceParameters` 属性を `true` に設定します。  
  
3.  プロジェクト項目のコード ファイルで、必要に応じてパラメーターを含めます。  たとえば、次のパラメーターは、ファイル内で名前空間に対して安全なプロジェクト名が使用されることを指定します。  
  
    ```  
    namespace $safeprojectname$  
    ```  
  
## 予約済みテンプレート パラメーター  
 テンプレートで使用できる予約済みテンプレート パラメーターを次の表に示します。  
  
> [!NOTE]
>  テンプレート パラメーターでは、大文字と小文字が区別されます。  
  
|パラメーター|説明|  
|------------|--------|  
|`clrversion`|共通言語ランタイム \(CLR: Common Language Runtime\) の現在のバージョン。|  
|`GUID [1-10]`|プロジェクト ファイルでプロジェクト GUID を置き換えるために使用される GUID。  最大 10 の GUID を指定できます \(たとえば、`guid1)`。|  
|`itemname`|**\[新しい項目の追加\]** ダイアログ ボックスでユーザーが指定した名前。|  
|`machinename`|現在のコンピューター名 \(たとえば、Computer01\)。|  
|`projectname`|**\[新しいプロジェクト\]** ダイアログ ボックスでユーザーが指定した名前。|  
|`registeredorganization`|HKLM\\Software\\Microsoft\\Windows NT\\CurrentVersion\\RegisteredOrganization のレジストリ キー値。|  
|`rootnamespace`|現在のプロジェクトのルート名前空間。  このパラメーターは、項目テンプレートにのみ適用されます。|  
|`safeitemname`|**\[新しい項目の追加\]** ダイアログ ボックスでユーザーが指定した名前から、安全でないすべての文字とスペースを削除したもの。|  
|`safeprojectname`|**\[新しいプロジェクト\]** ダイアログ ボックスでユーザーが指定した名前から、安全でないすべての文字とスペースを削除したもの。|  
|`time`|DD\/MM\/YYYY 00:00:00 の形式で表した現在の時間。|  
|`SpecificSolutionName`|ソリューションの名前。  \[ソリューションのディレクトリを作成\] がオンになっている場合は、`SpecificSolutionName` にソリューション名が指定されます。  \[ソリューションのディレクトリを作成\] がオフになっている場合、`SpecificSolutionName` は空白です。|  
|`userdomain`|現在のユーザー ドメイン。|  
|`username`|現在のユーザー名。|  
|`webnamespace`|現在の Web サイトの名前。  このパラメーターは、Web フォーム テンプレートで一意のクラス名を保証するために使用されます。  この Web サイトが Web サーバーのルート ディレクトリにある場合、このテンプレート パラメーターは Web サーバーのルート ディレクトリとして解決されます。|  
|`year`|YYYY の形式で表した現在の年。|  
  
## カスタム テンプレート パラメーター  
 パラメーター置換時に使用される既定の予約済みテンプレート パラメーターの他に、独自のテンプレート パラメーターと値を指定できます。詳細については、「[CustomParameters 要素 \(Visual Studio テンプレート\)](../extensibility/customparameters-element-visual-studio-templates.md)」を参照してください。  
  
## 例: ファイル名の置換  
 `TargetFileName` 属性を指定してパラメーターを使用することにより、プロジェクト項目に対して変数ファイル名を指定できます。  たとえば、.exe ファイルが `$projectname$` によって指定されるプロジェクト名をファイル名として使用するように指定できます。  
  
```  
<TemplateContent>  
    <ProjectItem  
        ReplaceParameters="true"  
        TargetFileName="$projectname$.exe">  
            File1.exe  
    </ProjectItem>  
      ...  
</TemplateContent>  
```  
  
## 例: 名前空間名に対するプロジェクト名の使用  
 Visual C\# クラス ファイル Class1.cs で名前空間に対してプロジェクト名を使用するには、次の構文を使用します。  
  
```  
#region Using directives  
  
using System;  
using System.Collections.Generic;  
using System.Text;  
  
#endregion  
  
namespace $safeprojectname$  
{  
    public class Class1  
        {  
            public Class1()  
                {  
  
                }  
         }  
}  
```  
  
 プロジェクト テンプレートの .vstemplate ファイルで、ファイル Class1.cs を参照するときに次の XML を含めます。  
  
```  
<TemplateContent>  
    <ProjectItem ReplaceParameters="true">  
        Class1.cs  
    </ProjectItem>  
    ...  
</TemplateContent>  
```  
  
## 参照  
 [テンプレートのカスタマイズ](../ide/customizing-project-and-item-templates.md)