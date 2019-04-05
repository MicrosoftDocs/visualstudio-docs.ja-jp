---
title: 開く を使用してコマンド ファイルの表示 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open With command
- Open With command
- persistence, supporting Open With command
ms.assetid: 53794bc3-1b73-4d40-954e-cfade1abddcf
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0f8e5e368199a3c554499a0ca01cbb66e51fab84
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58978113"
---
# <a name="displaying-files-by-using-the-open-with-command"></a>プログラムから開くコマンドを使用したファイルの表示
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プロジェクトを表示するための IDE を問い合わせることができる、**プログラムから開く** ダイアログ ボックス。 この要求には、ユーザーを標準のエディターの選択範囲を持つファイルを開くことが求められます。 次の手順では、このプロセスについて説明します。  
  
1.  プロジェクト呼び出し<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>、OSE_UseOpenWithDialog の値を指定する、`OSEOpenDocEditor`パラメーター。  
  
2.  IDE、ドキュメントのファイル名拡張子に基づいて、レジストリに一覧表示するエディターは、指定されたドキュメントを開くかを決定およびでは、この情報が表示されます、**ファイルを開く** ダイアログ ボックス。  
  
    > [!NOTE]
    >  プロジェクトに含める必要がある組み込みのエディターを**プログラムから開く** ダイアログ ボックスはそのような各エディターのエディター ファクトリを登録する必要があります。 組み込みエディター機能の実装で実施されるプロジェクトの特定の種類と共に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>メソッド。 IDE では、コアのテキスト エディターとバイナリ エディターの組み込みエディター ファクトリがあります。 IDE には、各登録済みの Windows ファイルの関連付けの代わりには、エディター ファクトリのインスタンスも作成します。 このようなファイルの例は、Microsoft Word です。  
  
3.  ユーザーがから項目を選択するとすぐ、**プログラムから開く** ダイアログ ボックスで、IDE が呼び出すことによってドキュメントを開く<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>メソッド。 詳細については、「[方法 :標準のエディターを開く](../../extensibility/how-to-open-standard-editors.md)します。  
  
## <a name="see-also"></a>関連項目  
 [開くと、プロジェクト項目の保存](../../extensibility/internals/opening-and-saving-project-items.md)   
 [ファイルを開くコマンドを使用してファイルを表示します。](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)   
 [方法: 標準のエディターを開く](../../extensibility/how-to-open-standard-editors.md)
