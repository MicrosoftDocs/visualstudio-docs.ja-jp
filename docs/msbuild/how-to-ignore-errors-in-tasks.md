---
title: "方法: タスクで発生したエラーを無視する | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSBuild, ignoring errors
- ContinueOnError attribute [MSBuild]
ms.assetid: e2f1ca4f-787b-44bd-bc64-81a036025e96
caps.latest.revision: 18
author: kempb
ms.author: kempb
manager: ghogen
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 3ba7680d46345f2b49019659c715cfb418933d39
ms.openlocfilehash: 263a2cdc87b46a70d9114a830955a54cde85d527

---
# <a name="how-to-ignore-errors-in-tasks"></a>方法 : タスクで発生したエラーを無視する
ビルド時に一部のタスクのエラーを許容するとよい場合があります。 そのような重要でないタスクが失敗しても必要な出力は生成できるため、ビルドを続行させる場合です。 たとえば、各コンポーネントのビルド後にプロジェクトで `SendMail` タスクを使ってメール メッセージを送信する場合、メール サーバーが利用できず、ステータス メッセージを送信できなくても、完了までビルドを続行させるのは許容範囲と見なせる場合があります。 別の例として、通常、ビルド中に中間ファイルが削除される場合、それらのファイルを削除できなくても、完了までビルドを続行させるのは許容範囲と見なせる場合があります。  
  
## <a name="using-the-continueonerror-attribute"></a>ContinueOnError 属性の使用  
 `Task` 要素の `ContinueOnError` 属性は、タスク エラーの発生時にビルドを停止するか続行するかを制御します。 この属性は、ビルドを続行するときに、エラーをエラーとして扱うか、それとも警告として扱うかも制御します。  
  
 `ContinueOnError` 属性には、次の値のいずれかを含めることができます。  
  
-   **WarnAndContinue** または **true**。 タスクが失敗すると、[Target](../msbuild/target-element-msbuild.md) 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーが警告として扱われます。  
  
-   **ErrorAndContinue**。 タスクが失敗すると、`Target` 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーがエラーとして扱われます。  
  
-   **ErrorAndStop** または **false** (既定値)。 タスクが失敗すると、`Target` 要素の残りのタスクとビルドは実行されず、`Target` 要素全体とビルドは失敗したと見なされます。  
  
 バージョン 4.5 より前の .NET Framework では、`true` 値と `false` 値のみがサポートされます。  
  
 `ContinueOnError` の既定値は `ErrorAndStop` です。 属性を `ErrorAndStop` に設定すると、プロジェクト ファイルを読むユーザーにとって動作は明確になります。  
  
#### <a name="to-ignore-an-error-in-a-task"></a>タスクのエラーを無視するには  
  
-   タスクの `ContinueOnError` 属性を使用します。 例:  
  
     `<Delete Files="@(Files)" ContinueOnError="WarnAndContinue"/>`  
  
## <a name="example"></a>例  
 次のコード例は、`Delete` タスクが失敗した場合でも `Build` ターゲットが実行され続け、ビルドが成功したと見なされることを示します。  
  
```xml  
<Project DefaultTargets="FakeBuild"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <Files Include="*.obj"/>  
    </ItemGroup>  
    <Target Name="Clean">  
        <Delete Files="@(Files)" ContinueOnError="WarnAndContinue"/>  
    </Target>  
  
    <Target Name="FakeBuild" DependsOnTargets="Clean">  
        <Message Text="Building after cleaning..."/>  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>関連項目
[MSBuild](../msbuild/msbuild.md)  
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)   
 [タスク](../msbuild/msbuild-tasks.md)


<!--HONumber=Feb17_HO4-->


