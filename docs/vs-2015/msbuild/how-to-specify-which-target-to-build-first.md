---
title: '方法: 最初にビルドするターゲットを指定する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- DefaultTargets attribute [MSBuild]
- MSBuild, specifying the defalut target
- MSBuild, DefaultTargets attribute
ms.assetid: a580ba5b-2919-42d2-ae38-1af991e0205a
caps.latest.revision: 20
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 52baabe5a8cf2e064c72ef7a5ab146d534214d90
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54797041"
---
# <a name="how-to-specify-which-target-to-build-first"></a>方法 : 最初にビルドするターゲットを指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
プロジェクト ファイルには、プロジェクトのビルド方法を定義する 1 つ以上の `Target` 要素を含めることができます。 [!INCLUDE[vstecmsbuildengine](../includes/vstecmsbuildengine-md.md)] ([!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]) エンジンは、見つけた最初のプロジェクトと依存関係をビルドします。ただし、プロジェクト ファイルに `DefaultTargets` 属性または `InitialTargets` 属性が含まれている場合や、コマンド ラインで **/target** スイッチを使ってターゲットが指定されている場合は例外です。  
  
## <a name="using-the-initialtargets-attribute"></a>InitialTargets 属性を使用する  
 `Project` 要素の `InitialTargets` 属性は、最初に実行するターゲットを指定します。これは、ターゲットがコマンド ラインまたは `DefaultTargets` 属性に指定されている場合でも変わりありません。  
  
#### <a name="to-specify-one-initial-target"></a>1 つの初期ターゲットを指定するには  
  
- `Project` 要素の `InitialTargets` 属性の既定のターゲットを指定します。 次に例を示します。  
  
   `<Project InitialTargets="Clean">`  
  
  ターゲットを順番に一覧表示し、セミコロンを使って各ターゲットを区切ることにより、`InitialTargets` 属性で複数の初期ターゲットを指定できます。 リスト内のターゲットは、順番に実行されます。  
  
#### <a name="to-specify-more-than-one-initial-target"></a>2 つ以上の初期ターゲットを指定するには  
  
-   `Project` 要素の `InitialTargets` 属性で、セミコロンで区切られた初期ターゲットを一覧表示します。 たとえば、`Clean` ターゲットを実行してから `Compile` ターゲットを実行する場合は、次を入力します。  
  
     `<Project InitialTargets="Clean;Compile">`  
  
## <a name="using-the-defaulttargets-attribute"></a>DefaultTargets 属性を使用する  
 `Project` 要素の `DefaultTargets` 属性は、ターゲットがコマンド ラインで明示的に指定されていない場合にビルドするターゲット (複数可) を指定します。 ターゲットが `InitialTargets` 属性と `DefaultTargets` 属性の両方で指定され、コマンド ラインではターゲットが指定されていない場合、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は、`InitialTargets` 属性で指定されたターゲットを実行し、次に `DefaultTargets` 属性で指定されたターゲットを実行します。  
  
#### <a name="to-specify-one-default-target"></a>1 つの既定のターゲットを指定するには  
  
- `Project` 要素の `DefaultTargets` 属性の既定のターゲットを指定します。 次に例を示します。  
  
   `<Project DefaultTargets="Compile">`  
  
  ターゲットを順番に一覧表示し、セミコロンを使って各ターゲットを区切ることにより、`DefaultTargets` 属性で複数の既定のターゲットを指定できます。 リスト内のターゲットは、順番に実行されます。  
  
#### <a name="to-specify-more-than-one-default-target"></a>2 つ以上の既定のターゲットを指定するには  
  
-   `Project` 要素の `DefaultTargets` 属性で、セミコロンで区切られた既定のターゲットを一覧表示します。 たとえば、`Clean` ターゲットを実行してから `Compile` ターゲットを実行する場合は、次を入力します。  
  
     `<Project DefaultTargets="Clean;Compile">`  
  
## <a name="using-the-target-switch"></a>/target スイッチを使用する  
 既定のターゲットがプロジェクト ファイルで定義されていない場合、またはその既定のターゲットを使用しない場合は、コマンド ライン スイッチ **/target** を使用して別のターゲットを指定できます。 `DefaultTargets` 属性で指定されたターゲットではなく、**/target** スイッチで指定されたターゲットが実行されます。 `InitialTargets` 属性で指定されたターゲットが常に最初に実行されます。  
  
#### <a name="to-use-a-target-other-than-the-default-target-first"></a>最初に既定のターゲット以外のターゲットを使用する  
  
-   **/target** コマンド ライン スイッチを使用してターゲットを最初のターゲットとして指定します。 次に例を示します。  
  
     `msbuild file.proj /target:Clean`  
  
#### <a name="to-use-several-targets-other-than-the-default-targets-first"></a>最初に既定のターゲット以外の複数のターゲットを使用するには  
  
-   **/target** コマンド ライン スイッチを使用して、セミコロンまたはコンマで区切られたターゲットを一覧表示します。 次に例を示します。  
  
     `msbuild <file name>.proj /t:Clean;Compile`  
  
## <a name="see-also"></a>関連項目
  [MSBuild](msbuild.md)  
 [ターゲット](../msbuild/msbuild-targets.md)   
 [方法 : ビルドをクリーンする](../msbuild/how-to-clean-a-build.md)
