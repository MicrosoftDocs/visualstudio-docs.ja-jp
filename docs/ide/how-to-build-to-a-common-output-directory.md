---
title: '方法: 共通出力ディレクトリへのビルド'
description: プロジェクトのビルド出力パスを変更し、すべての出力を強制的に同じフォルダーに配置する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
- output directory
- builds [Visual Studio], common directory
- common directory
ms.assetid: 1fcc2c48-07cb-4c4f-9556-36945e7dfc4e
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2e2abb9a768621477465b753554c111126a5af98
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99967619"
---
# <a name="how-to-build-to-a-common-output-directory"></a>方法: 共通出力ディレクトリへのビルド

既定では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] は、ソリューションの各プロジェクトを、そのソリューション内の独自のフォルダーにビルドします。 プロジェクトのビルド出力パスを変更して、すべての出力を強制的に同じフォルダーに配置することができます。

## <a name="to-place-all-solution-outputs-in-a-common-directory"></a>すべてのソリューション出力を共通ディレクトリに配置するには

1. ソリューションのいずれかのプロジェクトをクリックします。

2. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

3. プロジェクトの種類に応じて、**[コンパイル]** タブまたは **[ビルド]** タブのいずれかをクリックし、**[出力パス]** をそのソリューションのすべてのプロジェクトで使用するフォルダーに設定します。

4. ソリューションのすべてのプロジェクトに対して、手順 1 から 3 を繰り返します。

## <a name="see-also"></a>関連項目

- [コンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
- [方法: ビルド出力ディレクトリを変更する](../ide/how-to-change-the-build-output-directory.md)