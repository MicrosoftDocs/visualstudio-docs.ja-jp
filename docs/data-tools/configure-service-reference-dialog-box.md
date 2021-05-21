---
title: '[サービス参照の構成] ダイアログ ボックス'
description: Visual Studio の [サービス参照の構成] ダイアログ ボックスを使用して、Windows Communication Foundation (WCF) サービスの動作を構成します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- msvse_wcf.dlg.ConfigureServiceReference
helpviewer_keywords:
- WCF services, Configure Service Reference dialog box
- service references [Visual Studio], configuring behavior
- Configure Service Reference dialog box
ms.assetid: 25e4c36b-2db6-4e71-9010-b7068255d09d
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 9ce4057378db357345869d10e933929ae31ee573
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859217"
---
# <a name="configure-service-reference-dialog-box"></a>[サービス参照の構成] ダイアログ ボックス

**[サービス参照の構成]** ダイアログ ボックスでは、Windows Communication Foundation (WCF) サービスの動作を構成できます。

**[サービス参照の構成]** ダイアログ ボックスにアクセスするには、**ソリューション エクスプローラー** でサービス参照を右クリックし、**[サービス参照の構成]** を選択します。 **[サービス参照の追加] ダイアログ ボックス** で **[詳細]** ボタンをクリックしてダイアログ ボックスにアクセスすることもできます。

## <a name="task-list"></a>タスク一覧

- WCF サービスがホストされるアドレスを変更するには、**[アドレス]** フィールドに新しいアドレスを入力します。

- WCF クライアント内のクラスのアクセス レベルを変更するには、**[生成されたクラスのアクセス レベル]** リストでアクセス レベル キーワードを選択します。

- WCF サービスのメソッドを非同期に呼び出すには、**[非同期操作を生成する]** チェック ボックスをオンにします。

- WCF クライアントでメッセージ コントラクト型を生成するには、**[メッセージ コントラクトを常に生成]** チェック ボックスをオンにします。

- WCF クライアントのリストまたはディクショナリ コレクションの型を指定するには、**[コレクション型]** リストおよび **[ディクショナリ コレクション型]** リストから型を選択します。

- 型の共有を無効にするには、**[参照されたアセンブリで型を再利用]** チェック ボックスをオフにします。 参照されたアセンブリのサブセットで型の共有を有効にするには、**[参照されたアセンブリで型を再利用]** チェック ボックスをオンにし、**[参照されたアセンブリを指定して型を再利用]** チェック ボックスをオンにして、**[Referenced assemblies list]\(参照されたアセンブリの一覧\)** で必要な参照を選択します。

## <a name="uielement-list"></a>UIElement の一覧

**アドレス**

サービス参照でサービスを検索する Web アドレスを更新します。 たとえば、開発中のサービスは開発サーバーでホストされ、その後、運用サーバーに移行される場合があり、アドレスの変更が必要になります。

> [!NOTE]
> Address 要素は、**[サービス参照の構成]** ダイアログ ボックスが **[サービス参照の追加] ダイアログ ボックス** から表示された場合は使用できません。

**[生成されたクラスのアクセス レベル]**

WCF クライアント クラスのコード アクセス レベルを特定します。

> [!NOTE]
> Web サイト プロジェクトの場合、このオプションは常に `Public` に設定され、変更できません。 詳細については、「[サービス参照のトラブルシューティング](../data-tools/troubleshooting-service-references.md)」を参照してください。

**[非同期操作を生成する]**

WCF サービス メソッドの呼び出しが同期 (既定) または非同期のどちらであるかを指定します。

**[タスク ベースの操作を生成する]**

非同期コードを作成する場合、このオプションにより、.NET 4 で導入されたタスク並列ライブラリ (TPL) を利用できます。 「[タスク並列ライブラリ (TPL)](/dotnet/standard/parallel-programming/task-parallel-library-tpl)」を参照してください。

**[メッセージ コントラクトを常に生成]**

WCF クライアント向けにメッセージ コントラクト型を生成するどうかを指定します。 メッセージ コントラクトの詳細については、「[メッセージ コントラクトの使用](/dotnet/framework/wcf/feature-details/using-message-contracts)」を参照してください。

**[コレクション型]**

WCF クライアントのリスト コレクション型を指定します。 既定の型は <xref:System.Array> です。

**[ディクショナリ コレクション型]**

WCF クライアントのディクショナリ コレクション型を指定します。 既定の型は <xref:System.Collections.Generic.Dictionary%602> です。

**[参照されたアセンブリで型を再利用]**

サービスが追加または更新されたときに、WCF クライアントが新しい型を生成するのではなく、参照されたアセンブリ内の既存の型を再利用するかどうかを指定します。 既定では、このチェック ボックスはオンになっています。

**[参照されたアセンブリすべてで型を再利用]**

選択すると、 **[Referenced assemblies list]\(参照されたアセンブリの一覧\)** のすべての型が可能であれば再利用されます。 既定では、このオプションが選択されています。

**[参照されたアセンブリを指定して型を再利用]**

選択すると、 **[Referenced assemblies list]\(参照されたアセンブリの一覧\)** で選択された型だけが再利用されます。

**[Referenced assemblies list]\(参照されたアセンブリの一覧\)**

プロジェクトまたは Web サイトの参照されたアセンブリの一覧が含まれます。 **[参照されたアセンブリを指定して型を再利用]** を選択すると、個々のアセンブリを選択または選択解除できます。

**[Web 参照の追加]**

**[Web 参照の追加]** ダイアログ ボックスを表示します。

> [!NOTE]
> このオプションは、.NET Framework のバージョン 2.0 をターゲットとするプロジェクトでのみ使用する必要があります。
>
> [!NOTE]
> **[Web 参照の追加]** ボタンは、 **[サービス参照の構成]** ダイアログ ボックスが **[サービス参照の追加]** ダイアログ ボックスから表示された場合にのみ使用できます。

## <a name="see-also"></a>関連項目

- [方法 : Web サービスへの参照を追加する](how-to-add-update-or-remove-a-wcf-data-service-reference.md)
- [Windows Communication Foundation サービスと WCF Data Services](../data-tools/configure-service-reference-dialog-box.md)
