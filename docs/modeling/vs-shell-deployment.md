---
title: VS Shell 配置
description: 分離シェルを使用して、DSL の操作に必要な Visual Studio 機能と、そのソリューションの外観について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1293593e71aa57d8e74b9035320b3da5108aba09
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99924213"
---
# <a name="vs-shell-deployment"></a>VS Shell 配置

分離シェルを使用すると、ドメイン固有言語の操作に必要な Visual Studio 機能と、そのソリューションの外観がわかります。 Visual Studio の分離シェルの詳細については、[分離シェルのカスタマイズ](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)に関するページを参照してください。

Visual Studio シェルを配置ターゲットとして設定するには:

1. **[DslPackage]** プロジェクトで、**source.extension.tt** を開きます。

2. `<SupportedProducts>` の下に次を挿入します。

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   *MyIsolatedShell* を、お使いの分離シェル パッケージに名前に変更します。