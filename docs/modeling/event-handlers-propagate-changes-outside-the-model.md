---
title: イベント ハンドラーによって変更内容がモデル外に反映される
description: 視覚化およびモデリング SDK でストア イベント ハンドラーを定義して、ストアの外部のリソースに変更を反映させることができることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, events
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0ed45d631697d37db8da49e459e80f1b5a43a373
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99935132"
---
# <a name="event-handlers-propagate-changes-outside-the-model"></a>イベント ハンドラーによって変更内容がモデル外に反映される

視覚化およびモデリング SDK でストア イベント ハンドラーを定義して、ストアの外部にあるリソースに変更を反映できます (ストア以外の変数、ファイル、他のストア内のモデル、他の Visual Studio 拡張機能など)。 ストア イベント ハンドラーは、トリガー イベントが発生したトランザクションの終了後に実行されます。 それらは、[元に戻す] 操作または [やり直す] 操作でも実行されます。 そのため、ストア ルールとは異なり、ストア イベントは、ストアの外部にある値を更新する場合に最も役立ちます。 .NET イベントとは異なり、ストア イベント ハンドラーはクラスをリッスンするように登録されます。インスタンスごとに個別のハンドラーを登録する必要はありません。 変更を処理するさまざまな方法を選択する方法の詳細については、「[変更に対する応答と反映](../modeling/responding-to-and-propagating-changes.md)」を参照してください。

グラフィック画面やその他のユーザー インターフェイス コントロールは、ストア イベントによって処理できる外部リソースの例です。

### <a name="to-define-a-store-event"></a>ストア イベントを定義するには

1. 監視するイベントの種類を選択します。 完全な一覧については、<xref:Microsoft.VisualStudio.Modeling.EventManagerDirectory> のプロパティを参照してください。 各プロパティは、イベントの種類に対応します。 最も頻繁に使用されるイベントの種類は次のとおりです。

    - `ElementAdded` -モデル要素、リレーションシップ リンク、シェイプ、またはコネクタが作成されたときにトリガーされます。

    - ElementPropertyChanged - `Normal` ドメイン プロパティの値が変更されたときにトリガーされます。 イベントは、新しい値と古い値が等しくない場合にのみトリガーされます。 計算されたストレージ プロパティとカスタム ストレージ プロパティにこのイベントを適用することはできません。

         リレーションシップ リンクに対応するロール プロパティには適用できません。 代わりに、`ElementAdded` を使用してドメイン リレーションシップを監視します。

    - `ElementDeleted` - モデル要素、リレーションシップ、図形、またはコネクタが削除された後にトリガーされます。 要素のプロパティ値には引き続きアクセスできますが、他の要素とのリレーションシップはなくなります。

2. **DslPackage** プロジェクト内の別のコード ファイルに _YourDsl_**DocData** の部分クラス定義を追加します。

3. 次の例に示すように、イベントのコードをメソッドとして記述します。 `DocData` にアクセスする場合を除き、`static` にすることができます。

4. `OnDocumentLoaded()` をオーバーライドしてハンドラーを登録します。 複数のハンドラーがある場合は、それらすべてを同じ場所に登録できます。

登録コードの場所は重要ではありません。 場所として `DocView.LoadView()` を選択できます。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.VisualStudio.Modeling;

namespace Company.MusicLib
{
  partial class MusicLibDocData
  {
    // Register store events here or in DocView.LoadView().
    protected override void OnDocumentLoaded()
    {
      base.OnDocumentLoaded(); // Don't forget this.

      #region Store event handler registration.
      Store store = this.Store;
      EventManagerDirectory emd = store.EventManagerDirectory;
      DomainRelationshipInfo linkInfo = store.DomainDataDirectory
          .FindDomainRelationship(typeof(ArtistAppearsInAlbum));
      emd.ElementAdded.Add(linkInfo,
          new EventHandler<ElementAddedEventArgs>(AddLink));
      emd.ElementDeleted.Add(linkInfo,
          new EventHandler<ElementDeletedEventArgs>(RemoveLink));

      #endregion Store event handlers.
    }

    private void AddLink(object sender, ElementAddedEventArgs e)
    {
      ArtistAppearsInAlbum link = e.ModelElement as ArtistAppearsInAlbum;
      if (link != null)
            ExternalDatabase.Add(link.Artist.Name, link.Album.Title);
    }
    private void RemoveLink(object sender, ElementDeletedEventArgs e)
    {
      ArtistAppearsInAlbum link = e.ModelElement as ArtistAppearsInAlbum;
      if (link != null)
            ExternalDatabase.Delete(link.Artist.Name, link.Album.Title);
    }
  }
}
```

## <a name="use-events-to-make-undoable-adjustments-in-the-store"></a>イベントを使用してストアで取り消し可能な調整を行う

イベント ハンドラーはトランザクションがコミットされた後に実行されるため、通常は、ストア内の変更を反映するのにストア イベントは使用されません。 代わりに、ストア ルールを使用します。 詳細については、「[ルールによってモデル内の変更が反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。

ただし、ユーザーが元のイベントとは別に追加の更新を元に戻せるようにする場合は、イベント ハンドラーを使用してストアに対する追加の更新を行うことができます。 たとえば、アルバム タイトルは小文字であることが通例であるとします。 ユーザーによってタイトルが大文字で入力された後、それを小文字に修正するストア イベント ハンドラーを記述できます。 ただし、ユーザーは、[元に戻す] コマンドを使用して、修正をキャンセルして大文字を復元できます。 2 回目の [元に戻す] によって、ユーザーの変更が削除されます。

これに対し、同じことを行うストア ルールを記述した場合、ユーザーによる変更とそれを修正する操作は同じトランザクション内で行われるため、ユーザーは元の変更を失うことなく調整を元に戻すことはできません。

```csharp
partial class MusicLibDocView
{
    // Register store events here or in DocData.OnDocumentLoaded().
    protected override void LoadView()
    {
      /* Register store event handler for Album Title property. */
      // Get reflection data for property:
      DomainPropertyInfo propertyInfo =
        this.DocData.Store.DomainDataDirectory
        .FindDomainProperty(Album.TitleDomainPropertyId);
      // Add to property handler list:
      this.DocData.Store.EventManagerDirectory
        .ElementPropertyChanged.Add(propertyInfo,
        new EventHandler<ElementPropertyChangedEventArgs>
             (AlbumTitleAdjuster));

      /*
      // Alternatively, you can set one handler for
      // all properties of a class.
      // Your handler has to determine which property changed.
      DomainClassInfo classInfo = this.Store.DomainDataDirectory
           .FindDomainClass(typeof(Album));
      this.Store.EventManagerDirectory
          .ElementPropertyChanged.Add(classInfo,
        new EventHandler<ElementPropertyChangedEventArgs>
             (AlbumTitleAdjuster));
       */
      return base.LoadView();
    }

// Undoable adjustment after a property is changed.
// Method can be static since no local access.
private static void AlbumTitleAdjuster(object sender,
         ElementPropertyChangedEventArgs e)
{
  Album album = e.ModelElement as Album;
  Store store = album.Store;

  // We mustn't update the store in an Undo:
  if (store.InUndoRedoOrRollback
      || store.InSerializationTransaction)
      return;

  if (e.DomainProperty.Id == Album.TitleDomainPropertyId)
  {
    string newValue = (string)e.NewValue;
    string lowerCase = newValue.ToLowerInvariant();
    if (!newValue.Equals(lowerCase))
    {
      using (Transaction t = store.TransactionManager
            .BeginTransaction("adjust album title"))
      {
        album.Title = lowerCase;
        t.Commit();
      } // Beware! This could trigger the event again.
    }
  }
  // else other properties of this class.
}
```

ストアを更新するイベントを記述する場合:

- [元に戻す] でモデル要素が変更されないようにするには、`store.InUndoRedoOrRollback` を使用します。 トランザクション マネージャーによって、ストア内のすべてのものが元の状態に戻ります。

- モデルがファイルから読み込まれている間に変更が行われないようにするには、`store.InSerializationTransaction` を使用します。

- 変更を加えると、さらにイベントがトリガーされます。 無限ループにならないようにしてください。

## <a name="store-event-types"></a>ストア イベントの種類

各イベントの種類は、Store.EventManagerDirectory のコレクションに対応しています。 イベント ハンドラーはいつでも追加または削除できますが、通常はドキュメントの読み込み時に追加します。

|`EventManagerDirectory` プロパティ名|実行するタイミング|
|-|-|
|ElementAdded|ドメイン クラス、ドメイン リレーションシップ、図形、コネクタ、または図のインスタンスが作成されます。|
|ElementDeleted|モデル要素がストアの要素ディレクトリから削除され、リレーションシップのソースまたはターゲットではなくなります。 要素は実際にはメモリから削除されず、今後の [元に戻す] に備えて保持されます。|
|ElementEventsBegun|外側のトランザクションの終了時に呼び出されます。|
|ElementEventsEnded|他のすべてのイベントが処理されたときに呼び出されます。|
|ElementMoved|モデル要素は、あるストア パーティションから別のストア パーティションに移動されています。<br /><br /> これは、図の図形の位置とは関係ありません。|
|ElementPropertyChanged|ドメイン プロパティの値が変更されています。 これは、古い値と新しい値が等しくない場合にのみ実行されます。|
|RolePlayerChanged|リレーションシップの 2 つのロール (両端) のいずれかが、新しい要素を参照しています。|
|RolePlayerOrderChanged|複数要素の接続性が 1 より大きいロールで、リンクの順序が変更されています。|
|TransactionBeginning||
|TransactionCommitted||
|TransactionRolledBack||

## <a name="see-also"></a>こちらもご覧ください

- [変更内容への対応および変更内容の反映](../modeling/responding-to-and-propagating-changes.md)
- [サンプル コード: サーキット ダイアグラム](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
