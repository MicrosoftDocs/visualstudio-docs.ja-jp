---
title: セキュリティで保護されたデプロイ
description: 証明書を使用してソリューションに署名するか、ClickOnce 信頼プロンプト キーを使用して、信頼の決定の基礎となる証拠を提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- deploying applications [Office development in Visual Studio], security
- Office development in Visual Studio, security
- Office applications [Office development in Visual Studio], security
- ClickOnce deployment [Office development in Visual Studio], security
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c778ed98a3f5d17007acccd2f16208ece3237037
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99906744"
---
# <a name="secure-deployment"></a>セキュリティで保護されたデプロイ
  Office ソリューションを作成すると、開発用コンピューターが自動的に更新され、プロジェクト内のコードが実行できるようになります。 ただし、ソリューションを配置する際は、証明書を使用してソリューションに署名するか、[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 信頼プロンプト キーを使用して、信頼の決定の基礎となる証拠を提供する必要があります。 詳細については、「[Office ソリューションへの信頼の付与](../vsto/granting-trust-to-office-solutions.md)」を参照してください。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 ドキュメントレベルのカスタマイズでは、ドキュメントをネットワークの場所に配置する場合は、Office アプリケーションのセキュリティ センターにある信頼できる場所の一覧にドキュメントの場所を追加する必要もあります。 エンドユーザーのコンピューターに対するドキュメントのアクセス許可を設定する方法の詳細については、「[ドキュメントへの信頼の付与](../vsto/granting-trust-to-documents.md)」を参照してください。

## <a name="prevent-office-solutions-from-running-code"></a>Office ソリューションでコードを実行できないようにする
 管理者は、レジストリを使用して、すべての Office ソリューションがコンピューター上で実行されないようにすることができます。 マネージド コード拡張機能を持つ Office ソリューションが開かれると、Visual Studio Tools for Office ランタイムによって、コンピューター上の次のいずれかのレジストリ キーの下に `Disabled` という名前のエントリが存在するかどうかが確認されます。

- **HKEY_CURRENT_USER\Software\Microsoft\VSTO**

- **HKEY_LOCAL_MACHINE\Software\Microsoft\VSTO**

  Office ソリューションでコードを実行できないようにするには、これらのレジストリ キーのいずれかまたは両方の下に `Disabled` エントリを作成し、`Disabled` 用の次のデータ型と値のいずれかを指定します。

- "0" (ゼロ) 以外の任意の文字列に設定されている REG_SZ または REG_EXPAND_SZ。

- 0 (ゼロ) 以外の値に設定されている REG_DWORD。

  Office ソリューションでコードを実行できるようにするには、両方の `Disabled` エントリを 0 (ゼロ) に設定するか、このレジストリ エントリを削除します。

## <a name="see-also"></a>関連項目
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)
- [Office ソリューションを実行またはホストするためのコンピューターの準備](/previous-versions/bb772092(v=vs.110))
- [Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)