---
title: '&lt;trustInfo&gt; 要素 (ClickOnce アプリケーション) | Microsoft Docs'
description: trustInfo 要素は、アプリケーションをクライアント コンピューター上で実行するのに必要な最低限のセキュリティ権限について説明するものです。 trustInfo 要素は必須です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#IPermission
- urn:schemas-microsoft-com:asm.v2#PermissionSet
- urn:schemas-microsoft-com:asm.v2#assemblyRequest
- urn:schemas-microsoft-com:asm.v2#trustInfo
- urn:schemas-microsoft-com:asm.v2#defaultAssemblyRequest
- urn:schemas-microsoft-com:asm.v2#security
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- manifests [ClickOnce], trustInfo element
- <trustInfo> element [ClickOnce application manifest]
ms.assetid: 8a813a74-e158-4308-be78-565937f6af83
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3e91bdb2e842692224564374e3f9f4d23cf71cf8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99945020"
---
# <a name="lttrustinfogt-element-clickonce-application"></a>&lt;trustInfo&gt; 要素 (ClickOnce アプリケーション)
アプリケーションをクライアント コンピューター上で実行するのに必要な最低限のセキュリティ権限について説明します。

## <a name="syntax"></a>構文

```xml

      <trustInfo>
   <security>
      <applicationRequestMinimum>
         <PermissionSet
            ID
            Unrestricted>
            <IPermission
               class
               version
               Unrestricted
            />
         </PermissionSet>
         <defaultAssemblyRequest
            permissionSetReference
         />
         <assemblyRequest
            name
            permissionSetReference
         />
      </applicationRequestMinimum>
      <requestedPrivileges>
         <requestedExecutionLevel
            level
            uiAccess
         />
      </requestedPrivileges>
   </security>
</trustInfo>
```

## <a name="elements-and-attributes"></a>要素と属性
 `trustInfo` 要素は必須です。この要素は `asm.v2` 名前空間にあります。 これには、属性はなく次の要素を含みます。

## <a name="security"></a>security
 必須。 この要素は `trustInfo` 要素の子です。 `applicationRequestMinimum` 要素を含み、属性はありません。

## <a name="applicationrequestminimum"></a>applicationRequestMinimum
 必須。 この要素は `security` 要素の子であり、 `PermissionSet`、 `assemblyRequest`、および `defaultAssemblyRequest`要素を含んでいます。 この要素には属性はありません。

## <a name="permissionset"></a>PermissionSet
 必須。 この要素は `applicationRequestMinimum` 要素の子であり、 `IPermission` 要素を含んでいます。 この要素には、次の属性があります。

- `ID`

     必須。 アクセス許可セットを識別します。 この属性は任意の値にできます。 この ID は `defaultAssemblyRequest` および `assemblyRequest` 属性で参照されます。

- `version`

     必須。 アクセス許可のバージョンを識別します。 通常、この値は `1`です。

## <a name="ipermission"></a>IPermission
 省略可能。 この要素は `PermissionSet` 要素の子です。 `IPermission` 要素には、.NET Framework 内のアクセス許可クラスを正しく指定します。 `IPermission` 要素には次の属性がありますが、アクセス許可クラスのプロパティに対応する追加の属性を持つことができます。 アクセス許可の具体的な構文については、Security.config ファイル内の例を参照してください。

- `class`

     必須。 アクセス許可クラスを厳密な名前で指定します。 たとえば、次のコードでは `FileDialogPermission` 型を指定しています。

     `System.Security.Permissions.FileDialogPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`

- `version`

     必須。 アクセス許可のバージョンを識別します。 通常、この値は `1`です。

- `Unrestricted`

     必須。 アプリケーションの実行に、このアクセス許可を無制限で与える必要があるかどうかを指定します。 `true`に設定すると、アクセス許可は無条件に与えられます。 `false`に設定するか、この属性を定義しない場合は、 `IPermission` タグで定義されているアクセス許可固有の属性に従って制限されます。 アクセス許可の例を次に示します。

    ```xml
    <IPermission
      class="System.Security.Permissions.EnvironmentPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
      version="1"
      Read="USERNAME" />
    <IPermission
      class="System.Security.Permissions.FileDialogPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
      version="1"
      Unrestricted="true" />
    ```

     この例の <xref:System.Security.Permissions.EnvironmentPermission> の宣言では、アプリケーションのアクセス許可を環境変数 USERNAME の読み取りのみに制限しています。これに対し、 <xref:System.Security.Permissions.FileDialogPermission> の宣言では、アプリケーションにすべての <xref:System.Windows.Forms.FileDialog> クラスを無制限に使用できるようにしています。

## <a name="defaultassemblyrequest"></a>defaultAssemblyRequest
 省略可能。 すべてのアセンブリに付与されるアクセス許可のセットを指定します。 この要素は `applicationRequestMinimum` 要素の子であり、以下の属性があります。

- `permissionSetReference`

     必須。 既定のアクセス許可として使用するアクセス許可セットの ID を指定します。 アクセス許可セットは、 `PermissionSet` 要素で宣言します。

## <a name="assemblyrequest"></a>assemblyRequest
 省略可能。 特定のアセンブリのアクセス許可を識別します。 この要素は `applicationRequestMinimum` 要素の子であり、以下の属性があります。

- `Name`

     必須。 アセンブリ名を識別します。

- `permissionSetReference`

     必須。 このアセンブリに必要なアクセス許可セットの ID を指定します。 アクセス許可セットは、 `PermissionSet` 要素で宣言します。

## <a name="requestedprivileges"></a>requestedPrivileges
 省略可能。 この要素は `security` 要素の子であり、 `requestedExecutionLevel` 要素を含んでいます。 この要素には属性はありません。

## <a name="requestedexecutionlevel"></a>requestedExecutionLevel
 省略可能。 アプリケーションを実行するために必要なセキュリティ レベルを指定します。 この要素には子はなく、次の属性があります。

- `Level`

   必須。 アプリケーションが要求するセキュリティ レベルを指定します。 次のいずれかの値になります。

   `asInvoker`。アクセス許可の追加要求は行いません。 このレベルでは、追加の信頼確認は不要です。

   `highestAvailable`。親プロセスが利用できる最上位のアクセス許可を要求します。

   `requireAdministrator`。完全な管理者のアクセス許可を要求します。

   [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、 `asInvoker`値のみでインストールされます。 それ以外の値でインストールすると、エラーが発生します。

- `uiAccess`

   省略可能。 アプリケーションが、保護されたユーザー インターフェイス要素へのアクセスを必要とするかどうかを指定します。 指定できる値は、 `true` または `false`です。既定値は false です。 署名付きのアプリケーションのみ、true の値を設定する必要があります。

## <a name="remarks"></a>解説
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションが、クライアント コンピューターによって既定で与えられる以上のアクセス許可を求める場合は、より高いレベルの信頼を与えるかどうかを確認するメッセージが、共通言語ランタイムの Trust Manager によって表示されます。 ユーザーが信頼を与えない場合、アプリケーションは実行されません。信頼を与えた場合は、ここで要求されたアクセス許可で実行されます。

 配置マニフェストに有効な信頼ライセンスがある場合には、 `defaultAssemblyRequest` や `assemblyRequest` を使用して要求されるすべてのアクセス許可は、ユーザーに確認することなく与えられます。

 アクセス許可の昇格の詳細については、「[ClickOnce アプリケーションのセキュリティ](../deployment/securing-clickonce-applications.md)」を参照してください。 ポリシー配置の詳細については、「 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)」を参照してください。

## <a name="examples"></a>例
 次の 3 つのコード例では、 `trustInfo` による配置のアプリケーション マニフェストで使用する、既定の名前付きセキュリティ ゾーン (Internet、LocalIntranet、および FullTrust) に対応する [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 要素を示しています。

 最初の例は、Internet セキュリティ ゾーンで使用できる既定のアクセス許可の `trustInfo` 要素を示しています。

```xml
<trustInfo>
    <security>
      <applicationRequestMinimum>
        <PermissionSet ID="Internet">
          <IPermission
            class="System.Security.Permissions.FileDialogPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Access="Open" />
          <IPermission
           class="System.Security.Permissions.IsolatedStorageFilePermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Allowed="DomainIsolationByUser"
            UserQuota="10240" />
          <IPermission
            class="System.Security.Permissions.SecurityPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Flags="Execution" />
          <IPermission
            class="System.Security.Permissions.UIPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Window="SafeTopLevelWindows"
            Clipboard="OwnClipboard" />
          <IPermission
            class="System.Drawing.Printing.PrintingPermission, System.Drawing, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"
            version="1"
            Level="SafePrinting" />
        </PermissionSet>
        <defaultAssemblyRequest permissionSetReference="Internet" />
      </applicationRequestMinimum>
    </security>
  </trustInfo>
```

 2 番目の例は、LocalIntranet セキュリティ ゾーンで使用できる既定のアクセス許可の `trustInfo` 要素を示しています。

```xml
<trustInfo>
    <security>
      <applicationRequestMinimum>
        <PermissionSet ID="LocalIntranet">
          <IPermission
            class="System.Security.Permissions.EnvironmentPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Read="USERNAME" />
          <IPermission
            class="System.Security.Permissions.FileDialogPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Unrestricted="true" />
          <IPermission
            class="System.Security.Permissions.IsolatedStorageFilePermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Allowed="AssemblyIsolationByUser"
            UserQuota="9223372036854775807"
            Expiry="9223372036854775807"
            Permanent="True" />
          <IPermission
            class="System.Security.Permissions.ReflectionPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Flags="ReflectionEmit" />
          <IPermission
            class="System.Security.Permissions.SecurityPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Flags="Assertion, Execution" />
          <IPermission
            class="System.Security.Permissions.UIPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Unrestricted="true" />
          <IPermission
            class="System.Net.DnsPermission, System, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1"
            Unrestricted="true" />
          <IPermission
            class="System.Drawing.Printing.PrintingPermission, System.Drawing, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"
            version="1"
            Level="DefaultPrinting" />
          <IPermission
            class="System.Diagnostics.EventLogPermission, System, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
            version="1" />
        </PermissionSet>
        <defaultAssemblyRequest permissionSetReference="LocalIntranet" />
      </applicationRequestMinimum>
    </security>
</trustInfo>
```

 3 番目の例は、FullTrust セキュリティ ゾーンで使用できる既定のアクセス許可の `trustInfo` 要素を示しています。

```xml
<trustInfo>
  <security>
    <applicationRequestMinimum>
      <PermissionSet ID="FullTrust" Unrestricted="true" />
      <defaultAssemblyRequest permissionSetReference="FullTrust" />
    </applicationRequestMinimum>
  </security>
</trustInfo>
```

## <a name="see-also"></a>関連項目
- [信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)