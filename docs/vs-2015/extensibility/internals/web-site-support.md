---
title: Web サイトのサポート |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- web site projects
ms.assetid: ce9f4266-bb64-4c09-be88-4bd6413f60d0
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f1a96504783de466551c6fb9d055b95ba38df760
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687690"
---
# <a name="web-site-support"></a>Web サイト サポート
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Web サイトのプロジェクト システムでは、Web プロジェクトを作成するプロジェクト システムです。 Web プロジェクトは、Web アプリケーションを作成します。 Web サイト プロジェクトでは、コードに関連付けられている各 Web ページの 1 つの実行可能ファイルを生成します。 場合は/App_Code フォルダー内のソース コード ファイルから追加の実行可能ファイルが生成されます。  
  
 Web サイト プロジェクト システムを作成するには、既存のプロジェクト システムへのテンプレートと登録属性を追加します。 これらの属性のいずれかの言語の IntelliSense のプロバイダーを選択します。 IntelliSense のプロバイダーの実装では、参照を処理し、キャッシュされていないスマート Web ページが要求されたときに、言語コンパイラを呼び出しています。  
  
 Web ページをコンパイルするために使用する言語コンパイラを登録する必要があります[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]します。 使用することができます、 [\<コンパイラ > 要素](https://msdn.microsoft.com/library/7a151659-b803-4c27-b5ce-1c4aa0d5a823)次の例のように、コンパイラを登録する Web.config ファイルで。  
  
```  
<system.codedom>  <compilers>    <compiler language="py;IronPython" extension=".py"       type="IronPython.CodeDom.PythonProvider, IronPython,       Version=1.0.2391.18146, Culture=neutral,       PublicKeyToken=b03f5f7f11d50a3a" />  </compilers></system.codedom>  
```  
  
## <a name="in-this-section"></a>このセクションの内容  
 [Web サイト サポートのテンプレート](../../extensibility/internals/web-site-support-templates.md)  
 新しい Web サイト プロジェクトと関連付けられている項目の作成に使用できるテンプレートの一覧を表示します。  
  
 [Web サイト サポートの属性](../../extensibility/internals/web-site-support-attributes.md)  
 Web サイト プロジェクトを接続する登録属性を表示します。[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]と[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]します。  
  
## <a name="related-sections"></a>関連項目  
 [Web プロジェクト](../../extensibility/internals/web-projects.md)  
 Web プロジェクト、Web サイト プロジェクトと Web application projects の 2 種類の概要を示します。
