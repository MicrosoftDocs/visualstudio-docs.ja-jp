---
title: 従来の言語サービスの自動書式設定 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services, automatic formatting
ms.assetid: c210fc94-77bd-4694-b312-045087d8a549
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e6183fc47138ebb5108e4fbbd2bfa407e5804a72
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157273"
---
# <a name="automatic-formatting-in-a-legacy-language-service"></a>従来の言語サービスの自動書式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

オート フォーマット、言語サービスでは、ユーザーが既知のコード コンストラクトの入力を開始するとのコード スニペットが自動的に挿入します。  
  
## <a name="automatic-formatting-behavior"></a>自動書式設定の動作  
 たとえば、「`if`言語サービスが自動的に一致する中かっこを挿入または、言語サービスが、かどうかに応じて、適切なインデント レベルに新しい行にカーソルを強制的場合は、ENTER キー押すと、前に、行は、新しいスコープが表示されます。  
  
 言語サービスの残りの部分に使用されるコマンドのフィルターは、自動書式設定するためも使用できます。 呼び出すことによって、対応する中かっこを強調することも<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A>します。  
  
## <a name="see-also"></a>関連項目  
 [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
