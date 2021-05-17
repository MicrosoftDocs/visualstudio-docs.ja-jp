---
title: シンボル プロバイダー | Microsoft Docs
description: 式エバリュエーターが変数と式を評価できるように、Visual Studio に用意されているシンボル プロバイダーについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- symbol handler
- debugging [Debugging SDK], symbol handler
ms.assetid: 5fce651b-fead-4418-81b0-a011df7644ab
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 132e3c15eed86c9008e49b74b6da6e5da5a3ce33
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079385"
---
# <a name="symbol-provider"></a>シンボル プロバイダー
式エバリュエーターの実装では、変数と式を評価するために、言語コンパイラによって生成されるシンボリック デバッグ情報にアクセスする必要があります。 これを行うには、シンボル ハンドラーとも呼ばれる、シンボル プロバイダー (SP) のインターフェイスを使用します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] には、プログラム データベース (PDB) シンボル ファイル形式を使用したマネージド コードとネイティブ コード用に SP が用意されています。 カスタム形式で格納されているシンボルをプログラムで使用する必要がある場合を除き、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に用意されている SP を使用することをお勧めします。

## <a name="implementation-notes"></a>実装に関するメモ
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグ エンジンでは、共通言語ランタイム (CLR) インターフェイスを使用して SP と通信することが想定されています。 そのため、Visual Studio デバッグ エンジンと連携する SP では、CLR をサポートしている必要があります。 すべての CLR デバッグ インターフェイスの完全な一覧については、[!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] に含まれる debugref.doc を参照してください。

 SP がカスタムのデバッグ エンジンとのみ連携する場合は、デバッグ エンジンのニーズによっては必要に応じて SP を実装できます。

## <a name="see-also"></a>関連項目
- [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)
