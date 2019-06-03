---
title: ワークフロー デザイナー:XAML をデバッグします。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d9305dbc-af62-4bdd-b03f-c54e3fe9ecc7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 0d22668089581dcf44609756a4e7f8f4527dd751
ms.sourcegitcommit: ba5e072c9fedeff625a1332f22dcf3644d019f51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66431818"
---
# <a name="how-to-debug-xaml-with-the-workflow-designer"></a>方法: ワークフロー デザイナーを使用して XAML をデバッグする

ワークフローは XAML で定義されます。 ワークフローの UI 表現は、ワークフローを定義する XAML ツリーに基づいて構築されます。 デバッグのエクスペリエンスは、ワークフロー デザイナーでワークフローのデバッグと似ています。 たとえば、XAML をデバッグ中にローカル、ウォッチ、およびスレッドのウィンドウ同様に機能のワークフロー デザイナーのデバッグとします。 また、XAML のデバッグ中に使用される呼び出し履歴ビューは、ワークフローの実行フローの行ベースの階層ビューです。

> [!NOTE]
> ワークフローの XAML がアクティビティと同じアセンブリ内にある場合、クラス名のアセンブリ部分は含まれません。 クラス (アクティビティ) 名のこの部分がないと、実行時に XAML を読み込むことはできません。 メイン プロジェクトと同じ名前空間でアクティビティを定義することはお勧めしません。定義した場合は、XAML をデザイナーで編集した後に手動で編集する必要があります。

## <a name="to-debug-workflow-xaml"></a>ワークフローの XAML をデバッグするには

1. Visual Studio では、ワークフローまたはアクティビティ プロジェクトを開きます。

2. アクティビティまたはアクティビティの説明に従って、デバッグするブレークポイントを設定[方法。ワークフロー内でブレークポイントを設定](../workflow-designer/how-to-set-breakpoints-in-workflows.md)します。

3. ワークフロー定義を含む選択 .xaml ファイルを右クリックして**コードの表示**します。 デザイン ビューでブレークポイントを設定したアクティビティの XAML 要素宣言と同じ行に、ブレークポイントが表示されます。

4. 」の説明に従ってデバッガーを起動[のワークフローをデバッグ](debugging-workflows-with-the-workflow-designer.md)します。

5. コードがいずれかのブレークポイントまで実行されると、そのブレークポイントに関連付けられている XAML 要素が強調表示されます。 次のブレークポイントに移動するには、使用、 **F10**または**F11**キー。

## <a name="see-also"></a>関連項目

- [方法: ワークフロー内のブレークポイントを設定する](../workflow-designer/how-to-set-breakpoints-in-workflows.md)
- [ワークフローをデバッグします。](debugging-workflows-with-the-workflow-designer.md)