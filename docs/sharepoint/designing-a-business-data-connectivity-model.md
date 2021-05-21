---
title: ビジネス データ接続モデルの設計 | Microsoft Docs
description: ビジネス データ接続 (BDC) モデルを設計します。 エンティティとメソッドを追加します。 メソッド パラメーターを定義します。 フィルター記述子を追加します。 BDC モデルを検証します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], designing a model
- Business Data Connectivity service [SharePoint development in Visual Studio], designing a model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8fb1aa194688533855b7c5bd1d58a4e3b97ac749
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99948843"
---
# <a name="design-a-business-data-connectivity-model"></a>ビジネス データ接続モデルを設計する
  モデル ファイルにエンティティとメソッドを追加することで、ビジネス データ接続 (BDC) サービス用のモデルを開発できます。 エンティティは、データ フィールドのコレクションを記述します。 たとえば、エンティティはデータベース内のテーブルを表すことができます。 メソッドは、エンティティによって表されるデータの追加、削除、更新などのタスクを実行します。 詳細については、「[SharePoint へのビジネス データの統合](../sharepoint/integrating-business-data-into-sharepoint.md)」を参照してください。

## <a name="add-entities"></a>エンティティの追加
 Visual Studio の **ツールボックス** から BDC デザイナーに **エンティティ** をドラッグまたはコピーすることで、エンティティを追加できます。 詳細については、「[方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)」を参照してください。

 エンティティのフィールドをクラスに定義します。 たとえば、`Address` という名前のフィールドを `Customer` クラスに追加できます。 新しいクラスをプロジェクトに追加するか、オブジェクト リレーショナル デザイナー (O/R デザイナー) などのツールを使用して作成された既存のクラスを使用できます。 エンティティの名前とエンティティを表すクラスの名前は、一致している必要はありません。 モデル内にメソッドを定義するときに、クラスをエンティティに関連付けます。

## <a name="add-methods"></a>メソッドを追加する
 ユーザーがモデルに基づくリストまたは Web パーツの情報を表示、追加、更新、または削除すると、BDC サービスによってモデル内のメソッドが呼び出されます。 ユーザーが実行できるタスクごとに、モデルにメソッドを追加する必要があります。 **[BDC メソッドの詳細]** ウィンドウから、5 つの基本メソッドの種類のいずれかを選択することで、メソッドを作成します。 次の表で、BDC モデルの 5 つの基本的なメソッドについて説明します。

|Method|説明|
|------------|-----------------|
|Finder|エンティティ インスタンスのコレクションを返します。 ユーザーがリストまたは Web パーツを開いたときに呼び出されます。 詳細については、「[方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)」を参照してください。|
|SpecificFinder|特定のエンティティ インスタンスを返します。 ユーザーがリスト内の特定の項目の詳細を表示したときに呼び出されます。 詳細については、「[方法: 特定の Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)」を参照してください。|
|Creator|エンティティのデータ ソースに新しいデータを追加します。 モデルに基づくリストのリボン上の **[新しい項目]** ボタンをユーザーが選択したときに呼び出されます。 詳細については、「[方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)」を参照してください。|
|Updater|リスト内のデータを変更します。 ユーザーがリストの情報を更新したときに呼び出されます。 詳細については、「[方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)」を参照してください。|
|Deleter|データを削除します。 ユーザーがリストから項目を削除したときに呼び出されます。 詳細については、「[方法: Deleter メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)」を参照してください。|

## <a name="define-method-parameters"></a>メソッド パラメーターを定義する
 メソッドを作成すると、Visual Studio によって、メソッドの型に適した入力パラメーターと出力パラメーターが追加されます。 これらのパラメーターは単なるプレースホルダーです。 ほとんどの場合、パラメーターを変更して、正しい型のデータを渡すか返すようにする必要があります。 たとえば、既定では、Finder メソッドは文字列を返します。 ほとんどの場合、エンティティのコレクションを返すように Finder メソッドの戻りパラメーターを変更します。 パラメーターの型記述子を変更することで、これを実行できます。 型記述子は、パラメーターのデータ型を記述する属性のコレクションです。 詳細については、「[方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)」を参照してください。

 Visual Studio では、モデル内のパラメーター間で型記述子をコピーできます。 たとえば、`CustomerTD` という名前の型記述子を `GetCustomer` メソッドの戻りパラメーターとして定義できます。 **BDC エクスプローラー** で `CustomerTD` 型記述子をコピーし、その型記述子を `CreateCustomer` メソッドの入力パラメーターに貼り付けることができます。 これにより、同じ型記述子を複数回定義する必要がなくなります。

## <a name="method-instances"></a>メソッド インスタンス
 メソッドを作成すると、Visual Studio によって既定のメソッド インスタンスが追加されます。 メソッド インスタンスは、メソッドへの参照にパラメーターの既定値を追加したものです。 1 つのメソッドに、複数のメソッド インスタンスを含めることができます。 各インスタンスは、メソッド シグネチャと一連の既定値を組み合わせたものです。 詳細については、「[方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)」を参照してください。

 プロジェクトを実行すると、SharePoint リストのドロップダウン リストにメソッド インスタンスが表示されます。 ユーザーは、メソッド インスタンスを選択してデータを表示できます。

 メソッド インスタンスに既定値を追加するには、モデルの XML を直接変更する必要があります。 詳細については、[DefaultValue](/previous-versions/office/developer/sharepoint-2010/ee559319(v=office.14)) に関するページを参照してください。

## <a name="add-filter-descriptors"></a>フィルター記述子を追加する
 モデルのコンシューマーで、何らかの条件と一致するエンティティのインスタンスの取得が必要になることがあります。 この機能を有効にするために、メソッドにフィルター記述子を追加できます。 フィルター記述子を使用してメソッドの実行前にメソッドに値を渡すことによって、モデル コンシューマーで、メソッドの結果セットをフィルター処理できます。 詳細については、「[方法: 外部システムからのインスタンスを制限するために操作にフィルター パラメーターを追加する](/previous-versions/office/developer/sharepoint-2010/ee554889(v=office.14))」を参照してください。

 SharePoint には、ユーザーがフィルター値を提供できるようにする機能がいくつか用意されています。 たとえば、ビジネス データ Web パーツによって、フィルター テキスト ボックスが用意されます。 ユーザーは、テキスト ボックスに値を入力することで、リストのデータを制限できます。 メソッドにフィルター記述子を追加する方法の詳細については、「[方法: フィルター記述子を Finder メソッドに追加する](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)」を参照してください。

### <a name="filter-descriptor-properties"></a>フィルター記述子のプロパティ
 フィルター記述子の **[関連付けられている型記述子]** 、 **[名前]** 、および **[型]** プロパティの値を設定する必要があります。 それ以外のプロパティはすべて省略可能です。

 **[関連付けられている型記述子]** プロパティは、フィルター記述子を入力パラメーターに関連付けます。 ユーザーがフィルター値を指定すると、BDC サービスによって、入力パラメーターを使用してその値がメソッドに渡されます。

 **[型]** プロパティは、使用するフィルター パターンを表します。 SharePoint では、選択したフィルター パターンが、ユーザー インターフェイス (UI) に表示されるテキストに影響します。 たとえば、比較子フィルター パターンの場合、テキスト **is equal to** がコントロールとしてビジネス データ Web パーツに表示されます。 各フィルター パターンの詳細については、「[BDC でサポートされるフィルターの種類](/previous-versions/office/developer/sharepoint-2010/ee556392(v=office.14))」を参照してください。

 フィルター記述子のプロパティの詳細については、[FilterDescriptor](/previous-versions/office/developer/sharepoint-2010/ee557835(v=office.14)) に関する記事を参照してください。

### <a name="provide-default-values"></a>既定値を指定する
 ユーザーがフィルター値を指定しないことがあります。 メソッド インスタンスに既定値を追加するか、メソッドのコードに既定値を設定することで、既定値を用意できます。 メソッド インスタンスに既定値を追加する方法の詳細については、[MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14)) に関する記事を参照してください。 メソッドのコードで入力パラメーターの既定値を設定する方法の例については、「[方法: フィルター記述子を Finder メソッドに追加する](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)」を参照してください。

## <a name="validate-the-model"></a>モデルを検証する
 開発中にモデルを検証できます。 Visual Studio によって、モデルが想定どおりに動作しない原因となる可能性がある問題が特定されます。 これらの問題は、Visual Studio の **[エラー一覧]** に表示されます。

 BDC デザイナーのショートカット メニューを開き、 **[検証]** をクリックすることで、モデルを検証できます。 モデルにエラーが含まれている場合は、 **[エラー一覧]** に表示されます。 エラーが含まれているコードにカーソルをすばやく移動するには、一覧のエラーをダブルクリックします。 別の方法として、**F8** キーまたは **Shift**+**F8** キーを繰り返し押して、一覧のエラー内を順方向または逆方向に移動できます。

 モデルのルールに何らかの違反が含まれていると、検証エラーが発生する可能性があります。 たとえば、型記述子の **IsCollection** プロパティが **true** に設定されているが子の型記述子が存在しない場合、検証エラーが表示されます。 場合によっては、BDC モデルのルールを参照して、Visual Studio の **[エラー一覧]** に表示されるエラーを理解する必要があります。 BDC モデルのルールの詳細については、「[BDCMetadata スキーマ](/previous-versions/office/developer/sharepoint-2010/ee556387(v=office.14))」を参照してください。

## <a name="debug-the-solution-that-contains-the-model"></a>モデルを含むソリューションをデバッグする
 コードのデバッグは、Visual Studio でコードをデバッグするのと同じように実行できます。 コードをデバッグするには、コード内の任意の場所にブレークポイントを設定してから、デバッガーを起動します。 Visual Studio によって SharePoint サイトが開きます。 SharePoint で、ビジネス データを使用するリストまたは Web パーツを作成します。 その後、コードをステップ実行できます。 SharePoint プロジェクトのデバッグの詳細については、「[SharePoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」を参照してください。

 プロジェクトに追加するカスタム アセンブリのコードをデバッグすることもできます。 ただし、カスタム アセンブリのコードをデバッグするには、ソリューション パッケージにアセンブリを追加する必要があります。 詳細については、「[方法: アセンブリを追加および削除する](../sharepoint/how-to-add-and-remove-additional-assemblies.md)」を参照してください。

 プロジェクトへのカスタム アセンブリの追加の詳細については、「[方法: BDC 機能にカスタム アセンブリを含める](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)」を参照してください。

### <a name="configure-bdc-security"></a>BDC のセキュリティを構成する
 ソリューションをデバッグする前に、SharePoint でセキュリティ設定の変更が必要になる可能性があります。 これらの設定を変更するには、SharePoint 2010 サーバーの全体管理 Web サイトでビジネス データ接続サービス アプリケーションを開きます。 **[メタデータ ストアのアクセス許可の設定]** ダイアログ ボックスで、ユーザー アカウントを追加し、次のいずれかのオプションを選択します。

|タスク|オプション|
|----------|------------|
|モデルを BDC サービスに配置する。|編集|
|モデルで外部コンテンツ タイプ (エンティティ) を使用してリストと Web パーツを作成する。|クライアントで選択可能|
|エンティティ データを作成、読み取り、更新、および削除する。|実行|

 これらの設定の詳細については、「[ビジネス データ接続サービスの管理](/previous-versions/office/sharepoint-server-2010/ee661742(v=office.14))」を参照してください。

 個々のモデルまたは外部コンテンツ タイプに対してセキュリティ アクセス許可を設定することもできます。 モデルのセキュリティ アクセス許可を設定する方法の詳細については、「[BDC モデル管理](/previous-versions/office/sharepoint-server-2010/ee524073(v=office.14))」を参照してください。 外部コンテンツ タイプのセキュリティ アクセス許可を設定する方法の詳細については、「[外部コンテンツ タイプ管理](/previous-versions/office/sharepoint-server-2010/ee524076(v=office.14))」を参照してください。

> [!NOTE]
> ローカルの SharePoint サーバーでソリューションをデバッグするには、これらの設定を使用します。 運用 SharePoint サーバーで BDC 関連のセキュリティ設定を構成する方法の詳細については、「[ビジネス データ接続サービスのセキュリティの概要](/previous-versions/office/sharepoint-server-2010/ee661743(v=office.14))」を参照してください。

### <a name="retract-models-that-become-corrupt"></a>破損したモデルを取り消す
 デバッガーを初めて起動すると、Visual Studio によってモデル全体が SharePoint に配置されます。 その後は、Visual Studio によって SharePoint のモデルが更新され、配置間に加えられた変更が反映されます。

 SharePoint からモデルを完全に取り消す操作を Visual Studio で実行しなければならない状況が発生することがあります。 たとえば、モデルが破損することがあります。  モデルを SharePoint に再配置するには、モデルの **[増分更新]** プロパティを **[False]** に設定した後、デバッガーを起動します。 **BDC エクスプローラー** でモデルを表すノードを選択すると、 **[プロパティ]** ウィンドウに **[増分更新]** プロパティが表示されます。 既定では、モデルの名前は **BdcModel1** です。

### <a name="change-identifier-names-of-entities-in-the-model"></a>モデル内のエンティティの識別子名を変更する
 モデルの配置後に識別子の名前を変更すると、配置エラーが発生することがあります。 このエラーは、モデルの **[増分更新]** プロパティを **[False]** に設定することでは解決できません。 モデルを手動で取り消してから、ソリューションをもう一度配置する必要があります。 詳細については、「[SharePoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」を参照してください。 最初にモデルを配置する前に **[増分更新]** プロパティを **[False]** に設定することで、このエラーを回避できます。

## <a name="locate-documentation-for-bdc-model-elements"></a>BDC モデル要素のドキュメントを見つける
 Visual Studio では、作成する各エンティティ、メソッド、またはその他の項目の XML 要素がモデルに追加されます。 要素の属性は、 **[プロパティ]** ウィンドウにプロパティとして表示されます。 モデルの設計時に Visual Studio によって生成される要素と属性の詳細については、「[BDCMetadata スキーマ](/previous-versions/office/developer/sharepoint-2010/ee556387(v=office.14))」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)|BDC のモデルを視覚的に設計するために使用できるツールについて説明します。|
|[方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)|外部コンテンツ タイプ (エンティティ) をモデルに追加する方法を示します。|
|[方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)|ユーザーがリストまたは Web パーツのエンティティの一覧を表示できるようにするメソッドを追加する方法を示します。|
|[方法: 特定の Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)|ユーザーが特定のエンティティの詳細を表示できるようにするメソッドを追加する方法を示します。|
|[方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)|ユーザーがリストまたは Web パーツから直接データ ソースにレコードを追加できるようにするメソッドを追加する方法を示します。|
|[方法: Deleter メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)|ユーザーがリストまたは Web パーツのユーザー インターフェイス (UI) のオプションを使用して、データ ソースからデータを削除できるようにするメソッドを追加する方法を示します。|
|[方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)|ユーザーがデータ ソースのデータ レコードをリストまたは Web パーツから直接変更できるようにするメソッドを追加する方法を示します。|
|[方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)|Visual Studio の [メソッドの詳細] ウィンドウを使用して、入力パラメーターと戻りパラメーターをメソッドに追加する方法を示します。|
|[方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)|モデルのパラメーターのデータ型を定義する方法を示します。|
|[方法: メソッド インスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)|BDC で実行されるメソッドのインスタンスを作成する方法を示します。|
|[方法: Finder メソッドにフィルター記述子を追加する](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)|Finder メソッドによって返されるインスタンスの数をユーザーが制限できるようにする方法を示します。|
|[エンティティ間の関連付けの作成](../sharepoint/creating-an-association-between-entities.md)|モデル内のエンティティ間のリレーションシップを定義する方法について説明します。 ビジネス データ Web パーツ、外部リスト、およびカスタム アプリケーションによって、これらのデータ リレーションシップをユーザー インターフェイス (UI) に表示できます。|
|[方法: エンティティ間に関連付けを作成する](../sharepoint/how-to-create-an-association-between-entities.md)|モデル内のエンティティ間のリレーションシップを定義する方法を示します。|
|[チュートリアル: ビジネス データを使用した SharePoint での外部リストの作成](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)|SharePoint 外部リストに連絡先を表示するモデルを作成してテストする方法について、手順を追って説明します。|
|[SharePoint へのビジネス データの統合](../sharepoint/integrating-business-data-into-sharepoint.md)|BDC サービスのモデルの作成と設計の概要について説明します。|
