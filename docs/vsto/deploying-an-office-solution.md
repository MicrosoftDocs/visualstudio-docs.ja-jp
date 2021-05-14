---
title: Office ソリューションを配置する
description: ClickOnce または Windows インストーラーを使用して、Office ソリューションを配置できます。 ClickOnce を使用すると、ソリューションを配置するために必要な手順の数を減らすことができます。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], event viewer
- deploying applications [Office development in Visual Studio], event viewer
- Office applications [Office development in Visual Studio], deploying Office solutions
- Office development in Visual Studio, deploying Office solutions
- ClickOnce deployment [Office development in Visual Studio], troubleshooting
- deploying applications [Office development in Visual Studio], Office solutions (2007 system)
- Office development in Visual Studio, troubleshooting
- Office development in Visual Studio, event viewer
- ClickOnce deployment [Office development in Visual Studio], about ClickOnce solution deployments
- Office solutions [Office development in Visual Studio], deploying
- deploying applications [Office development in Visual Studio], troubleshooting
- solutions [Office development in Visual Studio], deploying Office solutions (2007 system)
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 07e4734916f312f40def034a78dd007310e96d9e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888902"
---
# <a name="deploy-an-office-solution"></a>Office ソリューションを配置する
  ClickOnce または Windows インストーラーを使用して、Office ソリューションを配置できます。 ClickOnce を使用すると、ソリューションを配置および更新するために必要な手順の数を減らすことができます。 Windows インストーラーを使用する場合は、ユーザーがソリューションをインストールする際に、ソリューションをどのようにインストールするか、およびセットアップ プログラムがどのページを表示するかを制御できます。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="deploy-a-solution-by-using-clickonce"></a>ClickOnce を使用してソリューションを配置する
 ClickOnce を使用してソリューションを配置するときは、ユーザーがインストールして実行できる中央の場所にソリューションを発行します。 新しいセットアップ プログラムをユーザーに配布しなくても、ソリューションを更新できます。  この配置オプションの方が簡単ですが、ユーザーにカスタム設定ページを表示できません。 また、複数のユーザーがいるコンピューターでは、ソリューションを複数回インストールする必要があります。 「[ClickOnce を使用して Office ソリューションを配置する](../vsto/deploying-an-office-solution-by-using-clickonce.md)」を参照してください。

## <a name="deploy-a-solution-by-using-windows-installer"></a>Windows インストーラーを使用してソリューションを配置する
 Windows インストーラーを使用してソリューションを配置するときは、ユーザーにセットアップ プログラムを配布し、ユーザーがそのプログラムを使用してソリューションをインストールします。 セットアップ プログラムを使用すると、現在のユーザーのみではなく、コンピューターのすべてのユーザーに同時にソリューションをインストールできます。 また、ユーザーがソリューションをインストールするときに表示されるオプションを、少し詳細に制御できます。 たとえば、使用許諾契約を表示したり、ユーザーがソリューションの特定のコンポーネントをインストールできるようにしたりすることができます。 ただし、ソリューションを更新する場合は、新しいセットアップ プログラムを配布する必要があります。 「[Windows インストーラーを使用した Office ソリューションの配置](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
- [ClickOnce を使用して Office ソリューションを配置する](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [Windows インストーラーを使用した Office ソリューションの配置](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)
- [Office ソリューションの配置のトラブルシューティング](../vsto/troubleshooting-office-solution-deployment.md)
