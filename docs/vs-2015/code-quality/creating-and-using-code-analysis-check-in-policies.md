---
title: コード分析チェックイン ポリシーの作成と |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis, check-in policies
ms.assetid: 3fa5a849-e05f-4e31-8ba3-b014c889d94d
caps.latest.revision: 41
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 3a8015eb672e87431a1d225221ff2321c41e041a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697046"
---
# <a name="creating-and-using-code-analysis-check-in-policies"></a>コード分析を用いたチェックイン ポリシーの作成と使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Team Foundation バージョン管理 (TFVC: Team Foundation Version Control) を使用すると、チーム プロジェクト内の .NET Framework とネイティブ (C/C++) コード プロジェクトに適したコード分析のチェックイン ポリシーを作成できます。 コード分析を用いたチェックイン ポリシーを使用することにより、コード ベースにチェックインされるコードを管理し、品質を高めることができます。  
  
 ローカルのビルドが最新の状態で、コード分析が最新のソース ファイル上で実行されている場合は、チェックイン ポリシーで合格と見なされます。 コード プロジェクト内で有効に設定されるコード分析については、少なくともチーム プロジェクトのチェックイン ポリシー内で定義された規則と同じ規則を定義する必要があります。 [チーム プロジェクトの設定] でエラーとして指定された規則は、コード プロジェクト内においてもエラーとして指定する必要があります。  
  
> [!IMPORTANT]
> コード分析チェックイン ポリシーを Web サイト プロジェクトに適用することはできません。 これらのポリシーは、Web アプリケーション プロジェクトに適用できます。  
  
 [!INCLUDE[esprscc](../includes/esprscc-md.md)]のチーム プロジェクトの設定を使用して、コード分析を用いたチェックイン ポリシーを作成します。 チェックイン ポリシーはチーム プロジェクトに対して指定され、適用されますが、コード分析はローカルの開発用コンピューター上の各コード プロジェクトに対して構成され、実行されます。 このセクションでは、コード分析を用いたチェックイン ポリシーをチーム プロジェクト用に指定する方法と、カスタム コード分析ポリシーをマネージド コード用に実装する方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [方法: 作成または標準のコード分析チェックイン ポリシーの更新](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md)  
 コード分析ポリシーをチーム プロジェクト用に設定および変更するための手順を説明します。  
  
 [マネージド コード用のカスタム チェックイン ポリシーの実装](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md)  
 カスタム規則セットをチーム プロジェクトのマネージ コード用に作成するための手順と、チェックイン ポリシーを使用してチーム プロジェクトのコード プロジェクトを同期する方法について説明します。  
  
 [コード分析を用いたチェックイン ポリシーに関するバージョンの互換性](../code-quality/version-compatibility-for-code-analysis-check-in-policies.md)  
 [!INCLUDE[vstsLong](../includes/vstslong-md.md)] の異なるバージョン間におけるコード分析チェックインの互換性の問題について説明します。  
  
 [方法: コード分析辞書をカスタマイズします。](../code-quality/how-to-customize-the-code-analysis-dictionary.md)  
 コード分析の名前付け規則で参照される辞書に単語とトークンを追加する方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [品質ゲートの設定と適用](https://msdn.microsoft.com/library/bdc5666e-6cf0-45b2-a0a1-133c3f61e852)  
  
 [チーム プロジェクト チェックイン ポリシーによるコード品質の向上](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md)
