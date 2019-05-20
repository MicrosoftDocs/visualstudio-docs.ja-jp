---
title: プロジェクト階層ノード (C++) の名前を変更する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- HierUtil7 sample [Visual Studio SDK], renaming project nodes
- project nodes, renaming in HierUtil7 sample
ms.assetid: cea5968e-e9f8-41a5-b068-622df542247c
caps.latest.revision: 12
manager: jillfra
ms.openlocfilehash: c7ad43fe1fd0e22cd94194d3079761de812b6ced
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686583"
---
# <a name="renaming-project-hierarchy-nodes-c"></a>プロジェクト階層ノード (C++) の名前の変更
プロジェクト フォルダーの階層ノードの名前を変更するには、アンマネージ c++ HierUtil7 プロジェクトのフレームワークを使用します。 詳細については、次を参照してください。 [HierUtil7 サンプル](https://msdn.microsoft.com/29c15184-a70c-4813-86c2-fb1d47442d11)します。  
  
## <a name="expanding-the-hierarchy-node"></a>階層ノードを展開します。  
  
#### <a name="to-expand-the-hierarchy-node-and-rename-the-folder"></a>階層ノードを展開し、フォルダーの名前を変更するには  
  
1. 次のメソッドを使用して、[階層] ノードを選択します。  
  
    ```  
    IfFailGo(pNode->ExtExpand(EXPF_SelectItem, GUID_MacroExplorer));  
    ```  
  
     `pNode` フォルダーに対応する階層のコンテナーと`EXPF_SelectItem`からは、<xref:Microsoft.VisualStudio.Shell.Interop.EXPANDFLAGS>列挙体。 `GUID_MacroExplorer` Vsshell.idl で定義されている GUID 定数の例を示します、`rguidPersistenceSlot`の関数のシグネチャで`ExtExpand`Hu_node.h で定義されている。  
  
    ```  
    HRESULT ExtExpand(EXPANDFLAGS expandflags, REFGUID rguidPersistenceSlot = GUID_SolutionExplorer) const;  
    ```  
  
     フォルダーで、Hu_node.h ファイルを検索する\<インストール ルート > \Program Files\VSIP 8.0\EnvSDK\common\hierutil7:  
  
2. 使用して名前の変更コマンドを送信することによって、フォルダーを名前します。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.PostExecCommand%2A>  
  
    ```  
    IfFailGo(srpVsUIShell->PostExecCommand(&guidVSStd97, cmdidRename, 0, NULL));  
    ```  
  
     `srpVsUIShell` <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>ポインター:`<IVsUIShell>``srpVsUIShell`します。 `guiVSStd97` コマンド グループの一意の識別子は、コマンドは、 `cmdidRename` Vsshlids.h で定義されているが属しています。  
  
## <a name="see-also"></a>関連項目  
 [プロジェクトの種類を作成します。](../extensibility/internals/creating-project-types.md)   
 [VSSDK のサンプル](../misc/vssdk-samples.md)