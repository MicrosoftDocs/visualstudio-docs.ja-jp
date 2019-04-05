---
title: 64 ビット アプリケーションの前提条件の展開 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [Visual Studio], 64-bit
- 64-bit [Visual Studio]
- 64-bit programming [Visual Studio]
- 64-bit applications [Visual Studio]
ms.assetid: 87399e20-5510-41e4-b5b7-4a87c5773f21
caps.latest.revision: 25
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3f416a22bc7cbdd374622c89a1826ebff8af9450
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58974357"
---
# <a name="deploying-prerequisites-for-64-bit-applications"></a>64 ビット アプリケーションの配置のための必要条件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ClickOnce の配置では、 64 ビット プラットフォームのアプリケーションのインストールをサポートします。 対象プラットフォームは、32 ビット プラットフォームの場合は **x86**、AMD64 命令セットと EM64T 命令セットをサポートするコンピューターの場合は **x64**、64 ビットの Itanium プロセッサの場合は **Itanium** です。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 64 ビット アプリケーションのインストール時の必須コンポーネントとして使用できる再頒布可能パッケージを次の表に示します。  
  
 64 ビット コンポーネントを含まない必須コンポーネントを選択した場合、選択したパッケージは 64 ビット プラットフォームで使用できないことを示す警告が表示される可能性があります。  
  
|再頒布可能パッケージ|x64 サポート|IA64 サポート|  
|---------------------|-----------------|------------------|  
|[!INCLUDE[vsto_runtime](../includes/vsto-runtime-md.md)]|はい|いいえ|  
|Visual C++ 2010 ランタイム ライブラリ (IA64)|いいえ|[はい]|  
|Visual C++ 2010 ランタイム ライブラリ (x64)|[はい]|いいえ|  
|Microsoft .NET Framework 4 (x86 および x64)|はい||  
|Microsoft .NET Framework 4 Client Profile (x86 および x64)|[はい]||  
  
## <a name="see-also"></a>関連項目  
 [アプリケーション、サービス、およびコンポーネントの配置](../deployment/deploying-applications-services-and-components.md)   
 [方法: ClickOnce アプリケーションと共に必須コンポーネントをインストールします。](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)   
 [64 ビット アプリケーション](http://msdn.microsoft.com/library/fd4026bc-2c3d-4b27-86dc-ec5e96018181)
