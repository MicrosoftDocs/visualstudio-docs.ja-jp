---
title: クラス デザイナーのエラー
ms.date: 11/04/2016
ms.topic: troubleshooting
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
- error messages, class diagrams
- Class Designer [Visual Studio], errors
- class diagrams, errors
ms.assetid: 79d70e70-704c-4255-ab68-c10d6949470e
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aadc0cfb66226f463ff8a2049d4dbf81e7bcf62b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62975555"
---
# <a name="class-designer-errors"></a>クラス デザイナーのエラー

**クラス デザイナー**はソース ファイルの場所を追跡しないため、プロジェクト構造を変更するか、プロジェクト内でソース ファイルを移動すると、**クラス デザイナー**が型を見失うことがあります。たとえば、typedef 型、基本クラス型、またはアソシエーション型のソースの型を変更する場合によくあります。 **クラス デザイナーはこの型を表示できません**などのエラーが発生することがあります。 エラーを修正するには、変更または再配置したソース コードをもう一度クラス ダイアグラムにドラッグして再表示します。

## <a name="resources"></a>リソース

以下のリソースで、その他のエラーや警告に関して役立つ情報を参照できます。

- 「[Visual C++ コードの使用](working-with-visual-cpp-code.md)」には、クラス ダイアグラムでの C++ の表示に関するトラブルシューティング情報が含まれます。
- [Visual Studio クラス デザイナー フォーラム](http://go.microsoft.com/fwlink/?LinkId=160754)は、**クラス デザイナー**に関する質問のためのフォーラムです。

## <a name="see-also"></a>関連項目

- [クラスと型の設計と表示](designing-and-viewing-classes-and-types.md)
