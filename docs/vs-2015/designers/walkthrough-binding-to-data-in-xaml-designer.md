﻿---
title: 'チュートリアル: XAML デザイナーでのデータへのバインド |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
f1_keywords:
- VS.XamlDesigner.DataBinding
ms.assetid: 1a99aeae-c3ef-407d-ba79-b8055489a43d
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c839350dd37f71d4f3368e077f4d9afe1b2bb2f4
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65701923"
---
# <a name="walkthrough-binding-to-data-in-xaml-designer"></a>チュートリアル: XAML デザイナーでのデータへのバインド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XAML デザイナーで、アートボードと [プロパティ] ウィンドウを使用してデータ バインディング プロパティを設定できます。 このチュートリアルの例では、データをコントロールにバインドする方法を示します。 具体的には、`ItemCount` という名前の [DependencyProperty](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.dependencyproperty.aspx) を持つ簡単なショッピング カート クラスを作成した後、`ItemCount` プロパティを [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) コントロールの **Text** プロパティにバインドする方法を説明します。  
  
### <a name="to-create-a-class-to-use-as-a-data-source"></a>データ ソースとして使用するクラスを作成するには  
  
1. **[ファイル]** メニューで、 **[新規]**、 **[プロジェクト]** をクリックします。  
  
2. **[新しいプロジェクト]** ダイアログ ボックスで、**[Visual C#]** ノードまたは **[Visual Basic]** ノードを選びます。次に、**[Windows デスクトップ]** ノードを展開し、**[WPF アプリケーション]** テンプレートを選びます。  
  
3. プロジェクトに **BindingTest** という名前を付けて、**[OK]** をクリックします。  
  
4. MainWindow.xaml.cs (または MainWindow.xaml.vb) ファイルを開き、次のコードを追加します。 C# では、このコードを `BindingTest` 名前空間 (ファイルの最後の閉じかっこの前) に追加します。 Visual Basic では、新しいクラスを追加します。  
  
    ```csharp  
    public class ShoppingCart : DependencyObject  
    {  
        public int ItemCount  
        {  
            get { return (int)GetValue(ItemCountProperty); }  
            set { SetValue(ItemCountProperty, value); }  
        }  
  
        public static readonly DependencyProperty ItemCountProperty =  
             DependencyProperty.Register("ItemCount", typeof(int),  
             typeof(ShoppingCart), new PropertyMetadata(0));  
    }  
  
    ```  
  
    ```vb  
    Public Class ShoppingCart  
        Inherits DependencyObject  
  
        Public Shared ReadOnly ItemCountProperty As DependencyProperty = DependencyProperty.Register(  
            "ItemCount", GetType(Integer), GetType(ShoppingCart), New PropertyMetadata(0))  
        Public Property ItemCount As Integer  
            Get  
                ItemCount = CType(GetValue(ItemCountProperty), Integer)  
            End Get  
            Set(value As Integer)  
                SetValue(ItemCountProperty, value)  
            End Set  
        End Property  
    End Class  
    ```  
  
     このコードでは、[PropertyMetadata](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.propertymetadata.aspx) オブジェクトを使って、既定の項目数の値を 0 に設定しています。  
  
5. **[ファイル]** メニューで、**[ビルド]**、**[ソリューションのビルド]** の順に選びます。  
  
### <a name="to-bind-the-itemcount-property-to-a-textblock-control"></a>ItemCount プロパティを TextBlock コントロールにバインドするには  
  
1. ソリューション エクスプローラーで、MainWindow.xaml のショートカット メニューを開き、**[デザイナーの表示]** を選びます。  
  
2. ツールボックスで、[グリッド](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.grid.aspx) コントロールを選んでフォームに追加します。  
  
3. `Grid` を選んだ状態で、[プロパティ] ウィンドウの **[DataContext]** プロパティの横にある **[新規作成]** ボタンを選びます。  
  
4. **[オブジェクトの選択]** ダイアログ ボックスで、**[すべてのアセンブリを表示する]** チェック ボックスがオフであることを確認し、**BindingTest** 名前空間の下にある **ShoppingCart** を選んで、**[OK]** ボタンを選びます。  
  
     次の図は、**[オブジェクトの選択]** ダイアログ ボックスで **ShoppingCart** 選んだ状態を示しています。  
  
     ![[オブジェクトの選択] ダイアログ ボックス](../designers/media/blendselectobject.PNG "BlendSelectObject")  
  
5. **[ツールボックス]** で、`TextBlock` コントロールを選んでフォームに追加します。  
  
6. `TextBlock` コントロールを選んだ状態で、[プロパティ] ウィンドウで **[Text]** プロパティの右側にあるプロパティ マーカーを選んでから、**[データ バインディングの作成]** を選びます。 (プロパティ マーカーは小さいボックスで表示されています。)  
  
7. [データ バインディングを作成] ダイアログ ボックスの **[パス]** ボックスで、**[ItemCount: (int32)]** プロパティを選び、**[OK]** を選びます。  
  
     次の図は、**[ItemCount]** プロパティを選んだ **[データ バインディングの作成]** ダイアログ ボックスです。  
  
     ![[データ バインディングの作成] ダイアログ ボックス](../designers/media/xaml-create-data-binding.png "xaml_create_data_binding")  
  
8. F5 キーを押してアプリを実行します。  
  
     `TextBlock` コントロールにより、既定値の 0 がテキストとして表示されます。  
  
## <a name="see-also"></a>関連項目
 [XAML デザイナーを使用した UI の作成](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)   
 [NIB:値コンバーター ダイアログ ボックスを追加します。](https://msdn.microsoft.com/c5f3d110-a541-4b55-8bca-928f77778af8)
