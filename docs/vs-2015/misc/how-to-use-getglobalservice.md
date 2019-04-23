---
title: '方法: GetGlobalService を使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- services, GetGlobalService
ms.assetid: 4cdf5ab5-9f09-4caf-9011-2dcb2c62f1b7
caps.latest.revision: 14
manager: jillfra
ms.openlocfilehash: 1c1fb48e4bb354ef403b39b0f1320ead92f43967
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60054368"
---
# <a name="how-to-use-getglobalservice"></a>方法: GetGlobalService を使用します。
場合によっては、ツール ウィンドウからサービスを取得するサービスを認識しませんが、サービス プロバイダーをコンテナーに配置されているか、またはしない配置されているコンテナーを制御したり必要があります。 たとえば、コントロール内からアクティビティ ログに書き込む可能性があります。 これらおよびその他のシナリオの詳細については、次を参照してください。[方法。サービスのトラブルシューティング](../extensibility/how-to-troubleshoot-services.md)します。  
  
 ほとんどを取得できます[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]静的を呼び出すことによってサービス<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>メソッド。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 派生したすべての VSPackage を初めて初期化されるキャッシュ サービス プロバイダーに依存<xref:Microsoft.VisualStudio.Shell.Package>が配置されています。 この条件が満たされるか、または null のサービスに対応することを保証する必要があります。  
  
 さいわい、<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>ほとんどの場合、正常に動作します。  
  
- VSPackage では、別の VSPackage にしか認識サービスを提供する場合、サービスを要求する VSPackage は、サービスが読み込まれるを提供する VSPackage の前に配置されてます。  
  
- ツール ウィンドウを作成する場合は、VSPackage によっては、ツール ウィンドウを作成する前に、VSPackage が配置されました。  
  
- VSPackage で作成したツール ウィンドウでコントロールのコンテナーがホストされている場合は、コントロールのコンテナーを作成する前に、VSPackage が配置されました。  
  
### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>ツール ウィンドウまたはコントロールのコンテナー内からサービスを取得するには  
  
- このコードをコンス トラクター、ツール ウィンドウ、またはコントロールのコンテナーに挿入します。  
  
     [!code-csharp[UseGetGlobalService#1](../snippets/csharp/VS_Snippets_VSSDK/usegetglobalservice/cs/getglobalservicepackage.cs#1)]
     [!code-vb[UseGetGlobalService#1](../snippets/visualbasic/VS_Snippets_VSSDK/usegetglobalservice/vb/getglobalservicepackage.vb#1)]  
  
     このコードは、SVsActivityLog サービスを取得しにキャスト、<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>インターフェイスで、アクティビティ ログに書き込むことができます。 例については、「[方法: アクティビティ ログを使用して、](../extensibility/how-to-use-the-activity-log.md)します。  
  
## <a name="see-also"></a>関連項目  
 [方法: サービスをトラブルシューティングします。](../extensibility/how-to-troubleshoot-services.md)   
 [使用して、サービスを提供します。](../extensibility/using-and-providing-services.md)   
 [サービスの基本情報](../extensibility/internals/service-essentials.md)