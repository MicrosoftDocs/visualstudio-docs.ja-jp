---
title: UML 図をイメージ ファイルにエクスポートする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: b29ce2a5-0ee3-4ab7-9aa3-13ca9c6b37a2
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7c04b8bd4ab956fe60191237910db35e2e463d3e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442948"
---
# <a name="export-uml-diagrams-to-image-files"></a>UML 図をイメージ ファイルにエクスポートする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML ドキュメントをエクスポートする[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]プログラムの制御下にあるイメージにします。 たとえば、このエクスポートをドキュメントの自動生成の一部として実行できます。  
  
 ドキュメントをイメージに手動でエクスポートする場合は、図から図形をコピーして Word などの他のプログラムに貼り付けることができます。 ドキュメントを XPS 形式にして印刷することもできます。 詳細については、次を参照してください。[ダイアグラムをイメージとしてエクスポート](../modeling/export-diagrams-as-images.md)します。  
  
## <a name="saving-an-image"></a>イメージの保存  
 次のコードでは、イメージをファイルに保存するショートカット メニュー コマンド ("コンテキスト メニュー コマンド" とも呼ばれる) を定義しています。  
  
> [!NOTE]
> このコードをメニュー コマンドとして機能させるには、このコードを MEF コンポーネントに組み込む必要があります。 詳細については、次を参照してください。[モデリング図にメニュー コマンドを定義](../modeling/define-a-menu-command-on-a-modeling-diagram.md)します。  
  
 このコードでは、最初に <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation.IShape.GetObject%2A> を使用して基になる実装の <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram> を取得します。 この型には <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.CreateBitmap%2A> メソッドがあります。  
  
```  
namespace SaveToImage  
{  
  using System.ComponentModel.Composition; // for [Import], [Export]  
  using System.Drawing; // for Bitmap  
  using System.Drawing.Imaging; // for ImageFormat  
  using System.Linq; // for collection extensions  
  using System.Windows.Forms; // for SaveFileDialog  
  using Microsoft.VisualStudio.Modeling.Diagrams;  
    // for Diagram  
  using Microsoft.VisualStudio.Modeling.ExtensionEnablement;  
    // for IGestureExtension, ICommandExtension, ILinkedUndoContext  
  using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;  
    // for IDiagramContext  
  using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
    // for designer extension attributes  
  
  /// <summary>  
  /// Called when the user clicks the menu item.  
  /// </summary>  
  // Context menu command applicable to any UML diagram   
  [Export(typeof(ICommandExtension))]  
  [ClassDesignerExtension]  
  [UseCaseDesignerExtension]  
  [SequenceDesignerExtension]  
  [ComponentDesignerExtension]  
  [ActivityDesignerExtension]  
  class CommandExtension : ICommandExtension  
  {  
    [Import]  
    IDiagramContext Context { get; set; }  
  
    public void Execute(IMenuCommand command)  
    {  
      // Get the diagram of the underlying implementation.  
      Diagram dslDiagram = Context.CurrentDiagram.GetObject<Diagram>();  
      if (dslDiagram != null)  
      {  
        string imageFileName = FileNameFromUser();  
        if (!string.IsNullOrEmpty(imageFileName))  
        {  
          Bitmap bitmap = dslDiagram.CreateBitmap(  
           dslDiagram.NestedChildShapes,  
           Diagram.CreateBitmapPreference.FavorClarityOverSmallSize);  
          bitmap.Save(imageFileName, GetImageType(imageFileName));  
        }  
      }  
    }  
  
    /// <summary>  
    /// Called when the user right-clicks the diagram.  
    /// Set Enabled and Visible to specify the menu item status.  
    /// </summary>  
    /// <param name="command"></param>  
    public void QueryStatus(IMenuCommand command)  
    {  
      command.Enabled = Context.CurrentDiagram != null   
        && Context.CurrentDiagram.ChildShapes.Count() > 0;  
    }  
  
    /// <summary>  
    /// Menu text.  
    /// </summary>  
    public string Text  
    {  
      get { return "Save To Image..."; }  
    }  
  
    /// <summary>  
    /// Ask the user for the path of an image file.  
    /// </summary>  
    /// <returns>image file path, or null</returns>  
    private string FileNameFromUser()  
    {  
      SaveFileDialog dialog = new SaveFileDialog();  
      dialog.AddExtension = true;  
      dialog.DefaultExt = "image.bmp";  
      dialog.Filter = "Bitmap ( *.bmp )|*.bmp|JPEG File ( *.jpg )|*.jpg|Enhanced Metafile (*.emf )|*.emf|Portable Network Graphic ( *.png )|*.png";  
      dialog.FilterIndex = 1;  
      dialog.Title = "Save Diagram to Image";  
      return dialog.ShowDialog() == DialogResult.OK ? dialog.FileName : null;  
    }  
  
    /// <summary>  
    /// Return the appropriate image type for a file extension.  
    /// </summary>  
    /// <param name="fileName"></param>  
    /// <returns></returns>  
    private ImageFormat GetImageType(string fileName)  
    {  
      string extension = System.IO.Path.GetExtension(fileName).ToLowerInvariant();  
      ImageFormat result = ImageFormat.Bmp;  
      switch (extension)  
      {  
        case ".jpg":  
          result = ImageFormat.Jpeg;  
          break;  
        case ".emf":  
          result = ImageFormat.Emf;  
          break;  
        case ".png":  
          result = ImageFormat.Png;  
          break;  
      }  
      return result;  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [ダイアグラムをイメージとしてエクスポートします。](../modeling/export-diagrams-as-images.md)   
 [モデリング図にメニュー コマンドを定義する](../modeling/define-a-menu-command-on-a-modeling-diagram.md)
