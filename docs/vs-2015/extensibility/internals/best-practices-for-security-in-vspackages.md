---
title: Vspackage ではセキュリティのベスト プラクティス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- security [Visual Studio SDK]
- security best practices, VSPackages
- best practices, security
ms.assetid: 212a0504-cf6c-4e50-96b0-f2c1c575c0ff
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 940644cd3950c38c6383371c1844b54b328acd0c
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697269"
---
# <a name="best-practices-for-security-in-vspackages"></a>VSPackage のセキュリティのベスト プラクティス
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

インストールする、[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]する、コンピューターには、管理者の資格情報のコンテキストで実行する必要があります。 セキュリティおよび配置の基本単位、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]アプリケーションは、 [Vspackage](../../extensibility/internals/vspackages.md)します。 使用して VSPackage を登録する必要があります[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]、資格情報を管理する必要があります。  
  
 管理者は、レジストリとファイル システムに書き込むと、任意のコードを実行する完全なアクセス許可があります。 開発、デプロイ、または VSPackage をインストールするこれらのアクセス許可が必要です。  
  
 インストールされているとすぐに VSPackage が完全に信頼されます。 この高レベルの VSPackage に関連付けられている権限、ためには、誤って悪意のある VSPackage をインストールすることはできます。  
  
 ユーザーは、信頼できるソースからのみ Vspackage をインストールすることを確認してください。 VSPackages を開発する企業の名前を指定し、それらに署名する必要があります厳密に、ユーザーのため、その改ざんを防止します。 企業の VSPackages を開発するには、web サービスを評価し、セキュリティの問題の修正のリモート インストールなど、外部依存関係を調べる必要があります。  
  
 詳細については、.NET Framework の安全なコーディングのガイドラインを参照してください。 ([https://msdn.microsoft.com/library/d55zzx87.aspx](https://msdn.microsoft.com/library/d55zzx87.aspx))。  
  
## <a name="see-also"></a>関連項目  
 [追加のセキュリティ](https://msdn.microsoft.com/library/44a5c651-6246-4310-b371-65378917c799)   
 [DDEX セキュリティ](https://msdn.microsoft.com/44a52a70-5c98-450e-993d-4a3b32f69ba8)
