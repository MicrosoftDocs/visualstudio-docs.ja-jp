---
title: Bridge to Kubernetes でマネージド ID を使用する方法
ms.technology: vs-azure
ms.date: 04/28/2021
ms.topic: conceptual
description: AKS クラスターで、Bridge to Kubernetes を使用して Azure Active Directory (Azure AD) のマネージド ID を使用する方法について説明します
monikerRange: '>=vs-2019'
manager: jmartens
author: ghogen
ms.author: ghogen
ms.openlocfilehash: e4847b25531b48c8200a2620ca3e975f9677c881
ms.sourcegitcommit: 60b7a6159045a44293043a519c8ea6d915bf2c31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2021
ms.locfileid: "108335101"
---
# <a name="use-managed-identity-with-bridge-to-kubernetes"></a>Bridge to Kubernetes でマネージド ID を使用する

AKS クラスターで[マネージド ID](/azure/active-directory/managed-identities-azure-resources/overview) セキュリティ機能を使用してシークレットとリソースへのアクセスをセキュリティで保護している場合、Bridge to Kubernetes には、これらの機能を使用できるように特別な構成が必要です。 ローカルの実行とデバッグが適切にセキュリティで保護されていることを確認するには、Azure Active Directory (AD) トークンをローカル コンピューターにダウンロードする必要があります。これには、Bridge to Kubernetes での特別な構成が必要です。 この記事では、Bridge to Kubernetes を構成して、マネージド ID を使用するサービスと連携させる方法について説明します。

## <a name="how-to-configure-your-service-to-use-managed-identity"></a>マネージド ID を使用するようにサービスを構成する方法

マネージド ID がサポートされているローカル コンピューターを有効にするには、*KubernetesLocalConfig.yaml* ファイルの `enableFeatures` セクションで、`ManagedIdentity` を追加します。 `enableFeatures` セクションがまだない場合は、追加します。

```yaml
enableFeatures:
    ManagedIdentity
```

> [!WARNING]
> Azure AD トークンがローカル コンピューターにフェッチされ、セキュリティ上のリスクが生じる可能性があるため、運用クラスターではなく開発クラスターを使用する場合は、Bridge to Kubernetes にのみマネージド ID を使用するようにしてください。

*KubernetesLocalConfig.yaml* ファイルがない場合は作成できます。[Bridge to Kubernetes の構成方法](configure-bridge-to-kubernetes.md)に関するページを参照してください。

## <a name="how-to-fetch-the-azure-active-directory-tokens"></a>Azure Active Directory トークンをフェッチする方法

トークンをフェッチする場合は、コードで <xref:Azure.Identity.DefaultAzureCredential> または <xref:Azure.Identity.ManagedIdentityCredential> のいずれかに依存していることを確認する必要があります。

次の C# コードでは、`ManagedIdentityCredential` を使用するときにストレージ アカウントの資格情報をフェッチする方法を示します。

```csharp
var credential = new ManagedIdentityCredential(miClientId);
Console.WriteLine("Created credential");
var containerClient = new BlobContainerClient(new Uri($"https://{accountName}.blob.windows.net/{containerName}"), credential);
Console.WriteLine("Created blob client");
```

次のコードでは、DefaultAzureCredential を使用するときにストレージ アカウントの資格情報をフェッチする方法を示します。

```csharp
var credential = new DefaultAzureCredential();
Console.WriteLine("Created credential");
var containerClient = new BlobContainerClient(new Uri($"https://{accountName}.blob.windows.net/{containerName}"), credential);
Console.WriteLine("Created blob client");
```

マネージド ID を使用して他の Azure リソースにアクセスする方法については、「[次のステップ](#next-steps)」セクションを参照してください。

## <a name="receive-azure-alerts-when-tokens-are-downloaded"></a>トークンがダウンロードされたときに Azure アラートを受け取る

サービスで Bridge to Kubernetes を使用するたびに、Azure AD トークンがローカル コンピューターにダウンロードされます。 このような場合に通知を受け取るように Azure アラートを有効にすることができます。 詳細については、「[Azure Defender の有効化](/azure/security-center/enable-azure-defender)」を参照してください。 (30 日間の試用期間が終了した後は) 料金が発生することに注意してください。

## <a name="next-steps"></a>次のステップ

マネージド ID を使用する AKS クラスターと連携するように Bridge to Kubernetes を構成したので、通常どおりデバッグを行うことができます。 [bridge-to-kubernetes.md#connect-to-your-cluster-and-debug-a-service] を参照してください。

マネージド ID を使用して Azure リソースにアクセスする方法の詳細については、次のチュートリアルを参照してください。

- [チュートリアル: Linux VM のシステム割り当てマネージド ID を使用して Azure Storage にアクセスする](/azure/active-directory/managed-identities-azure-resources/tutorial-linux-vm-access-storage)
- [チュートリアル: Linux VM のシステム割り当てマネージド ID を使用して Azure Data Lake Store にアクセスする](/azure/active-directory/managed-identities-azure-resources/tutorial-linux-vm-access-datalake)
- [チュートリアル:Linux VM のシステム割り当てマネージド ID を使用して Azure Key Vault にアクセスする](/azure/active-directory/managed-identities-azure-resources/tutorial-linux-vm-access-nonaad)

そのセクションには、他の Azure リソースにアクセスするためにマネージド ID を使用する他のチュートリアルもあります。

## <a name="see-also"></a>関連項目

[Azure Active Directory](/azure/active-directory/managed-identities-azure-resources/)
