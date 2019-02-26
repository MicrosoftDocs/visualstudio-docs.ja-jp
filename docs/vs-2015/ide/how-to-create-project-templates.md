---
title: '方法: プロジェクト テンプレートの作成 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- VS.ExportTemplateWizard
helpviewer_keywords:
- Visual Studio templates, creating project templates
- project templates, metadata files
- Visual Studio templates, project templates
- project templates, custom template locations
- project templates, creating
ms.assetid: a1a6999d-a34c-48a8-b1cf-027eb5c76398
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9a7a48039699c5bb35e07a21e5c5c3be8ae8585f
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54785914"
---
# <a name="how-to-create-project-templates"></a>方法 : プロジェクト テンプレートを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この手順に従うと、**[テンプレートのエクスポート]** ウィザードを使ってテンプレートを作成できます。テンプレートは .zip ファイルにパッケージ化されます。 また、テンプレートのエクスポート ウィザードの拡張機能を使って、または [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] に含まれるテンプレートで、配置が向上した VSIX ファイル形式でテンプレートを作成できます。または、テンプレートを手動で作成することもできます。  
  
### <a name="to-create-a-custom-project-template-with-the-standard-export-template-wizard"></a>標準のテンプレートのエクスポート ウィザードを使ってカスタム プロジェクト テンプレートを作成するには  
  
1.  プロジェクトを作成します。  
  
    > [!NOTE]
    >  テンプレートのソースとなるプロジェクトに名前を付けるときは、有効な識別子文字のみを使ってください。 名前に無効な文字が含まれるプロジェクトからエクスポートされたテンプレートでは、後でそのテンプレートを基にしてプロジェクトを作成したときに、コンパイル エラーが発生する可能性があります。 有効な識別子文字について詳しくは、「[Declared Element Names](http://msdn.microsoft.com/library/09d8843b-c0dc-4afe-9dab-87c439a69e66)」(宣言された要素の名前) をご覧ください。  
  
2.  プロジェクトを編集して、テンプレートとしてエクスポートできる状態にします。  
  
3.  必要に応じて、コード ファイルを編集し、パラメーター置換を行う場所を示します。 パラメーター置換の詳細については、次を参照してください。[方法。テンプレート内のパラメーターを置き換える](../ide/how-to-substitute-parameters-in-a-template.md)」を参照してください。  
  
4.  **[ファイル]** メニューの **[テンプレートのエクスポート]** をクリックします。 **[テンプレートのエクスポート]** ウィザードが開きます。  
  
5.  **[プロジェクト テンプレート]** をクリックします。  
  
6.  現在のソリューションに複数のプロジェクトがある場合は、テンプレートとしてエクスポートするプロジェクトを選択します。  
  
7.  **[次へ]** をクリックします。  
  
8.  アイコンと、テンプレートのプレビュー イメージを選択します。 これらは、**[新しいプロジェクト]** ダイアログ ボックスに表示されます。  
  
9. テンプレートの名前と説明を入力します。  
  
10. **[完了]** をクリックします。 プロジェクトが .zip ファイルにエクスポートされ、指定した出力場所に置かれます。また、選択した場合は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] にインポートされます。  
  
     [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] がインストールされている場合は、**VSIX プロジェクト** テンプレートを使うことで、完成したテンプレートを配置用に .vsix ファイルにラップすることができます。 詳しくは、「[VSIX プロジェクトのテンプレートの概要](../extensibility/getting-started-with-the-vsix-project-template.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)   
 [方法 : 項目テンプレートを作成する](../ide/how-to-create-item-templates.md)
