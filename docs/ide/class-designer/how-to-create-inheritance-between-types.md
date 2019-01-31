---
title: '方法: 型の間の継承を作成する (クラス デザイナー)'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.inheritanceline
helpviewer_keywords:
- inheritance, relationship defining
- relationships, defining inheritance
ms.assetid: 3786a21c-8022-4bf5-9d13-740fd354e93c
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0efcabfb5f7b76855a80ae69f50ec9c5282ccb2c
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54939011"
---
# <a name="how-to-create-inheritance-between-types-in-class-designer"></a>方法: クラス デザイナーで型の間の継承を作成する

**クラス デザイナー**を使用してクラス ダイアグラム上の 2 つの型間の継承関係を作成するには、基本型をその派生型 (複数可) に接続します。 継承関係は、2 つのクラス間、クラスとインターフェイス間、または 2 つのインターフェイス間で作成できます。

## <a name="to-create-an-inheritance-between-types"></a>型間で継承を作成するには

1.  **ソリューション エクスプローラー**のプロジェクトから、クラス ダイアグラム (.cd) ファイルを開きます。

     クラス ダイアグラムがない場合は、クラス ダイアグラムを作成します。 「[方法:プロジェクトにクラス ダイアグラムを追加する](how-to-add-class-diagrams-to-projects.md)」を参照してください。

2.  **[クラス デザイナー]** の **[ツールボックス]** で、**[継承]** をクリックします。

3.  クラス ダイアグラムで、必要な型間の継承線を次の間で描画します。

    -   派生クラスから基底クラスへ

    -   実装するクラスから実装されるインターフェイスへ

    -   拡張するインターフェイスから拡張されるインターフェイスへ

4.  必要に応じて、ジェネリック型からの派生型がある場合に、継承線をクリックします。 **[プロパティ]** ウィンドウで、ジェネリック型に必要な型と一致するように **[型の引数]** プロパティを設定します。

    > [!NOTE]
    > 親抽象クラスに少なくとも 1 つの抽象メンバーが含まれている場合、すべての抽象メンバーは非抽象継承クラスとして実装されます。
    >
    >  既存のジェネリック型を視覚化できますが、新しいジェネリック型は作成できません。 また、既存のジェネリック型の型パラメーターは変更できません。

## <a name="see-also"></a>関連項目

- [継承](/dotnet/csharp/programming-guide/classes-and-structs/inheritance)
- [継承の基本](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)
- [方法: 型の間の継承を表示する](how-to-view-inheritance-between-types.md)
- [クラス デザイナーの Visual C++ クラス](visual-cpp-classes.md)