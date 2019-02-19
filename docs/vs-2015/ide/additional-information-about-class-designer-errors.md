﻿---
title: クラス デザイナーのエラーに関する追加情報 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.CPlusPlusViewInDiagramNoTypeFound
- vs.classdesigner.CPlusPlusNoTypeFound
- vs.classdesigner.CannotShowBaseType
- vs.classdesigner.MatchOrphanTypesAtLoad
- vs.classdesigner.CannotShowType
- vs.classdesigner.AssociationTypeNotFoundError
- vs.classdesigner.ViewInDiagramNoTypesFound
- vs.classdesigner.CannotImplementInterface
- vs.classdesigner.CannotShowImplementedInterface
- vs.classdesigner.ViewInDiagramUnparsableTypeFound
- vs.classdesigner.AssociationTypeNotFound
- vs.classdesigner.CPlusPlusTypeCannotBeAdded
helpviewer_keywords:
- errors, class diagrams
- errors, Class Designer
- error messages, Class Designer
- Class Designer [Visual Studio], errors
- error messages, class diagrams
- class diagrams, errors
ms.assetid: 79d70e70-704c-4255-ab68-c10d6949470e
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 66a895b48051ed8797644b36d6f6663e1e35a8e6
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54783681"
---
# <a name="additional-information-about-class-designer-errors"></a>クラス デザイナーのエラーに関する追加情報
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

クラス デザイナーはソース ファイルの場所を追跡しないため、プロジェクト構造を変更するか、プロジェクト内でソース ファイルを移動すると、クラス デザイナーが型を見失うことがあります (特にソースの型が typedef 型、基本クラス型、またはアソシエーション型の場合)。 **クラス デザイナーはこの型を表示できません**などのエラーが発生することがあります。 エラーが発生した場合は、変更または再配置したソース コードをもう一度クラス ダイアグラムにドラッグして再表示します。  
  
 以下のリソースで、その他のエラーや警告に関して役立つ情報を参照できます。  
  
 [Visual C++ コードの使用 (クラス デザイナー)](../ide/working-with-visual-cpp-code-class-designer.md)  
 クラス ダイアグラムでの C++ の表示に関するトラブルシューティング情報が含まれます。  
  
 [Visual Studio クラス デザイナー フォーラム](http://go.microsoft.com/fwlink/?LinkId=160754)  
 クラス デザイナーに関する質問のためのフォーラムです。  
  
## <a name="see-also"></a>関連項目
 [クラスと型のデザインおよび表示](../ide/designing-and-viewing-classes-and-types.md)
