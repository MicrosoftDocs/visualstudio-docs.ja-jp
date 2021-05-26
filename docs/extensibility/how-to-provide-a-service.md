---
title: '方法: サービスを提供する | Microsoft Docs'
description: VSPackage では、他の Vspackage で使用できるサービスを提供できます。 VSPackage で Visual Studio にサービスを登録し、サービスを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- services, providing
ms.assetid: 12bc1f12-47b1-44f6-b8db-862aa88d50d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8391d6d08214f915d136f80130cf9167573c14eb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069895"
---
# <a name="how-to-provide-a-service"></a>方法: サービスを提供する
VSPackage では、他の Vspackage で使用できるサービスを提供できます。 サービスを提供するには、VSPackage で Visual Studio にサービスを登録し、サービスを追加する必要があります。

 <xref:Microsoft.VisualStudio.Shell.Package> クラスは、<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> と <xref:System.ComponentModel.Design.IServiceContainer> の両方を実装しています。 <xref:System.ComponentModel.Design.IServiceContainer> には、要求時にサービスを提供するコールバック メソッドを格納します。

 サービスの詳細については、「[サービスの基本情報](../extensibility/internals/service-essentials.md)」を参照してください。

> [!NOTE]
> VSPackage がアンロードされるとき、Visual Studio では、VSPackage で提供するサービスのすべての要求が配信されるまで待機します。 これらのサービスに対して新しい要求を行うことはできません。 <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A> メソッドを明示的に呼び出して、アンロード時にサービスを取り消すことはできません。

## <a name="implement-a-service"></a>サービスを実装する

1. VSIX プロジェクトを作成します ( **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]**  >  **[Visual C#]**  >  **[機能拡張]**  >  **[VSIX プロジェクト]** )。

2. VSPackage をプロジェクトに追加します。 **ソリューション エクスプローラー** でプロジェクト ノードを選択し、 **[追加]**  >  **[新しい項目]**  >  **[Visual C# アイテム]**  >  **[機能拡張]**  >  **[Visual Studio パッケージ]** の順にクリックします。

3. サービスを実装するには、次の 3 種類を作成する必要があります。

   - サービスを記述するインターフェイス。 これらのインターフェイスの多くは空です。つまり、メソッドはありません。

   - サービス インターフェイスを記述するインターフェイス。 このインターフェイスには、実装するメソッドが含まれています。

   - サービスとサービス インターフェイスの両方を実装するクラス。

     次の例に、3 つの種類の基本的な実装を示します。 サービス クラスのコンストラクターでは、サービス プロバイダーを設定する必要があります。

   ```csharp
   public class MyService : SMyService, IMyService
   {
       private Microsoft.VisualStudio.OLE.Interop.IServiceProvider serviceProvider;
       private string myString;
       public MyService(Microsoft.VisualStudio.OLE.Interop.IServiceProvider sp)
       {
           Trace.WriteLine(
                  "Constructing a new instance of MyService");
           serviceProvider = sp;
       }
       public void Hello()
       {
           myString = "hello";
       }
       public string Goodbye()
       {
          return "goodbye";
       }
   }
   public interface SMyService
   {
   }
   public interface IMyService
   {
       void Hello();
       string Goodbye();
   }

   ```

### <a name="register-a-service"></a>サービスを登録する

1. サービスを登録するには、サービスを提供する VSPackage に <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> を追加します。 たとえば次のようになります。

    ```csharp
    [ProvideService(typeof(SMyService))]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [Guid(VSPackage1.PackageGuidString)]
    public sealed class VSPackage1 : Package
    {. . . }
    ```

     この属性では、`SMyService` を Visual Studio に登録します。

    > [!NOTE]
    > 名前が同じ別のサービスを置き換えるサービスを登録するには、<xref:Microsoft.VisualStudio.Shell.ProvideServiceOverrideAttribute> を使用します。 サービスのオーバーライドは 1 つしか許可されないことに注意してください。

### <a name="add-a-service"></a>サービスの追加

1. VSPackage 初期化子で、サービスを追加し、サービスを作成するコールバック メソッドを追加します。 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> メソッドに対して行う変更は次のとおりです。

    ```csharp
    protected override void Initialize()
    {
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);

        ((IServiceContainer)this).AddService(typeof(SMyService), callback);
    . . .
    }
    ```

2. サービスを作成して返し、作成できない場合は null を返すコールバック メソッドを実装します。

    ```csharp
    private object CreateService(IServiceContainer container, Type serviceType)
    {
        if (typeof(SMyService) == serviceType)
            return new MyService(this);
        return null;
    }
    ```

    > [!NOTE]
    > Visual Studio では、サービスを提供する要求を拒否できます。 これは、別の VSPackage で既にサービスを提供している場合に行います。

3. サービスを取得し、そのメソッドを使用できるようになりました。 次の例は、初期化子でサービスを使用する方法を示していますが、サービスを使用する任意の場所でサービスを取得できます。

    ```csharp
    protected override void Initialize()
    {
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);

        ((IServiceContainer)this).AddService(typeof(SMyService), callback);

        MyService myService = (MyService) this.GetService(typeof(SMyService));
        myService.Hello();
        string helloString = myService.Goodbye();

        base.Initialize();
    }
    ```

     `helloString` の値は "Hello" にする必要があります。

## <a name="see-also"></a>関連項目
- [方法: サービスを取得する](../extensibility/how-to-get-a-service.md)
- [サービスを使用および提供する](../extensibility/using-and-providing-services.md)
- [サービスの基本情報](../extensibility/internals/service-essentials.md)
