---
title: MSBuild ターゲット | Microsoft Docs
description: MSBuild で、ターゲットを使用してタスクをグループ化し、ビルド プロセスを小さな単位に分割する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/13/2019
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, targets
ms.assetid: 8060b4d2-e4a9-48cf-a437-852649ceb417
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 294877e4884ae7b89f1e9d6f015c5c9213eba52d
ms.sourcegitcommit: 4908561809ad397c99cf204f52d5e779512e502c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112254824"
---
# <a name="msbuild-targets"></a>MSBuild ターゲット

ターゲットはタスクを特定の順序でグループ化し、ビルド プロセスを小さな単位に分割することを可能にします。 たとえば、あるターゲットは、ビルドの準備として、出力ディレクトリに含まれるすべてのファイルを削除し、別のターゲットは、プロジェクトに対する入力をコンパイルし、空のディレクトリに配置します。 タスクについて詳しくは、「[MSBuild タスク](../msbuild/msbuild-tasks.md)」をご覧ください。

## <a name="declare-targets-in-the-project-file"></a>プロジェクト ファイルでターゲットを宣言する

 ターゲットは、プロジェクト ファイル内で、[Target](../msbuild/target-element-msbuild.md) 要素を使用して宣言します。 たとえば、次の XML は Construct という名前のターゲットを作成し、Compile というアイテムの種類で Csc タスクを呼び出します。

```xml
<Target Name="Construct">
    <Csc Sources="@(Compile)" />
</Target>
```

 MSBuild プロパティと同様に、ターゲットは再定義できます。 たとえば、オブジェクトに適用された

```xml
<Target Name="AfterBuild" >
    <Message Text="First occurrence" />
</Target>
<Target Name="AfterBuild" >
    <Message Text="Second occurrence" />
</Target>
```

`AfterBuild` を実行すると、"Second occurrence" (2 番目の出現) のみが表示されます。これは `AfterBuild` の 2 番目の定義によって最初の出現が隠されるためです。

MSBuild はインポートの順序に依存するので、最後のターゲットの定義が使用されます。 ターゲットを再定義しても、組み込みターゲットが後で定義されるなら効果がありません。 SDK を使用するプロジェクトの場合、定義の順序は必ずしも明白ではありません。プロジェクト ファイルの終了後にターゲットのインポートが暗黙的に追加されるためです。

したがって、既存のターゲットの動作を拡張するには、次のように新しいターゲットを作成し、`BeforeTargets` を指定します (あるいは、適切であれば `AfterTargets` を指定します)。

```xml
<Target Name="MessageBeforePublish" BeforeTargets="BeforePublish">
  <Message Text="BeforePublish" Importance="high" />
</Target>
```

コードで関数に名前を付けるように、ターゲットにわかりやすい名前を付けます。

## <a name="target-build-order"></a>ターゲットのビルド順序

 あるターゲットへの入力が別のターゲットの出力に依存する場合、ターゲットの順序を指定する必要があります。
 
 ターゲットの実行順序はいくつかの方法で指定できます。

- 初期ターゲット

- 既定のターゲット

- 最初のターゲット

- ターゲットの依存関係

- `BeforeTargets` と `AfterTargets` (MSBuild 4.0)

1 つのビルドでターゲットが 2 回実行されることはありません。そのビルド内の後続のターゲットが先行するターゲットに依存している場合でも同じです。 ターゲットは一度実行されると、それ以上ビルドに影響しません。

ターゲットのビルド順序に関する詳細については、「[ターゲットのビルド順序](../msbuild/target-build-order.md)」を参照してください。

## <a name="target-batching"></a>ターゲットのバッチ処理

あるターゲット要素に、%(\<Metadata>) 形式でメタデータを指定する `Outputs` 属性が含まれている場合があります。 その場合、MSBuild は一意のメタデータ値ごとにターゲットを 1 回実行し、そのメタデータ値を含むアイテムをグループ化または "バッチ処理" します。 たとえば、オブジェクトに適用された

```xml
<ItemGroup>
    <Reference Include="System.Core">
      <RequiredTargetFramework>3.5</RequiredTargetFramework>
    </Reference>
    <Reference Include="System.Xml.Linq">
      <RequiredTargetFramework>3.5</RequiredTargetFramework>
    </Reference>
    <Reference Include="Microsoft.CSharp">
      <RequiredTargetFramework>4.0</RequiredTargetFramework>
    </Reference>
</ItemGroup>
<Target Name="AfterBuild"
    Outputs="%(Reference.RequiredTargetFramework)">
    <Message Text="Reference:
      @(Reference->'%(RequiredTargetFramework)')" />
</Target>
```

 RequiredTargetFramework メタデータによって参照項目をバッチ処理します。 このターゲットの出力は次のようになります。

```
Reference: 3.5;3.5
Reference: 4.0
```

 ターゲット バッチ処理が実際のビルドで利用されることはほとんどありません。 タスクのバッチが一般的です。 詳細については、「[MSBuild バッチ](../msbuild/msbuild-batching.md)」をご覧ください。

## <a name="incremental-builds"></a>インクリメンタル ビルド

 インクリメンタル ビルドは、対応する入力ファイルに対して最新の状態の出力ファイルを含むターゲットが実行されないように最適化されたビルドです。 ターゲット要素には、`Inputs` 属性と `Outputs` 属性の両方を含めることができます。ターゲットが入力として受け取る項目と出力として生成する項目をそれぞれ示します。

 すべての出力項目が最新の状態になっている場合、MSBuild はターゲットをスキップします。これがビルドのスピードを大幅に上げます。 これはターゲットのインクリメンタル ビルドと呼ばれています。 一部のファイルだけが最新の状態になっている場合、MSBuild は最新の項目なしでターゲットを実行します。 これはターゲットの部分的インクリメンタル ビルドと呼ばれています。 詳細については、「[インクリメンタル ビルド](../msbuild/incremental-builds.md)」を参照してください。

## <a name="default-build-targets"></a>既定のビルド ターゲット

Microsoft.Common.CurrentVersion.Targets のパブリック ターゲットを次に示します。

```
===================================================
Build
The main build entry point.
===================================================
<Target Name="Build"
        Condition=" '$(_InvalidConfigurationWarning)' != 'true' "
        DependsOnTargets="$(BuildDependsOn)"
        Returns="$(TargetPath)" />


===================================================
BeforeBuild
===================================================
<Target Name="BeforeBuild"/>


===================================================
AfterBuild
===================================================
<Target Name="AfterBuild"/>


===================================================
CoreBuild
The core build step calls each of the build targets.
===================================================
<Target Name="CoreBuild"
        DependsOnTargets="$(CoreBuildDependsOn)">


===================================================
Rebuild
Delete all intermediate and final build outputs, and then build the project from scratch.
===================================================
<Target Name="Rebuild"
        Condition=" '$(_InvalidConfigurationWarning)' != 'true' "
        DependsOnTargets="$(RebuildDependsOn)"
        Returns="$(TargetPath)"/>


===================================================
BeforeRebuild
===================================================
<Target Name="BeforeRebuild"/>


===================================================
AfterRebuild
===================================================
<Target Name="AfterRebuild"/>


===================================================
BuildGenerateSources
Set BuildPassReferences to enable P2P builds
===================================================
<Target Name="BuildGenerateSources"
        DependsOnTargets="BuildGenerateSourcesTraverse;$(BuildGenerateSourcesAction)" />


===================================================
BuildCompile
===================================================
<Target Name="BuildCompile"
        DependsOnTargets="BuildCompileTraverse;$(BuildCompileAction)" />


===================================================
BuildLink
===================================================
<Target Name="BuildLink"
        DependsOnTargets="BuildLinkTraverse;$(BuildLinkAction)" />


===================================================
CopyRunEnvironmentFiles
Copy environment files necessary to run the user's app to the final directory.
This is a public target that can be invoked by an IDE.
This may be used by an IDE to make the app.config file available for running
the target app.
===================================================
<Target
        Name="CopyRunEnvironmentFiles"
        DependsOnTargets="PrepareForBuild;SetWin32ManifestProperties;_CopyAppConfigFile;_CleanRecordFileWrites"/>


===================================================
Run
Run the final build output if it is a .EXE
===================================================
<Target
        Name="Run"
        DependsOnTargets="$(RunDependsOn)">


===================================================
BuildOnlySettings
This target is called only when doing a real build.  It is specifically not called during project load.
===================================================
<Target Name="BuildOnlySettings">


===================================================
PrepareForBuild
Prepare the prerequisites for building.
===================================================
<Target Name="PrepareForBuild"
        DependsOnTargets="$(PrepareForBuildDependsOn)">


===================================================
GetFrameworkPaths
Get the paths for the .NET Framework installation directory

These paths are not used directly by this .targets file but are available for pre and
post build steps.

This is a generally overriden target, for example it is overriden in the Microsoft.NETFramework.targets file
===================================================
<Target Name="GetFrameworkPaths"/>


===================================================
GetReferenceAssemblyPaths
Get the paths for the Reference Assemblies for the known versions of the
.NET Framework.

These paths are used by the build process in order to resolve the correct
assemblies from the various directories, and to support multi-targeting
===================================================
<Target Name="GetReferenceAssemblyPaths"
        DependsOnTargets="$(GetReferenceAssemblyPathsDependsOn)">


===================================================
AssignLinkMetadata
For items of a certain set of allowed types, make sure that
if they are defined in a file other than the project file, that 
they have "Link" metadata set to an appropriate default. 
===================================================
<Target Name="AssignLinkMetadata"
        Condition=" '$(SynthesizeLinkMetadata)' == 'true' ">


===================================================
PreBuildEvent
Run the pre-build event if there is one.
===================================================
<Target Name="PreBuildEvent"
        Condition="'$(PreBuildEvent)'!=''"
        DependsOnTargets="$(PreBuildEventDependsOn)">


===================================================
UnmanagedUnregistration
If the main assembly had previously been registered for COM interop, unregister it now.
We will re-register the new version after it has been built.
===================================================
<Target Name="UnmanagedUnregistration"
        Condition="(('$(_AssemblyTimestampBeforeCompile)' != '$(_AssemblyTimestampAfterCompile)' or '$(RegisterForComInterop)' != 'true' or '$(OutputType)' != 'library') or
                                ('$(_AssemblyTimestampBeforeCompile)' == '')) and
                                Exists('@(_UnmanagedRegistrationCache)')"
        DependsOnTargets="$(UnmanagedUnregistrationDependsOn)">


===================================================
GetTargetFrameworkVersion
This stand-alone target returns the target framework version (i.e. v3.5, v4.0, etc.)
that would be used if we built this project.
===================================================
<Target
        Name="GetTargetFrameworkVersion"
        Returns="$(TargetFrameworkVersion)" />


===================================================
ResolveReferences
===================================================
<Target Name="ResolveReferences"
        DependsOnTargets="$(ResolveReferencesDependsOn)"/>


===================================================
BeforeResolveReferences
===================================================
<Target Name="BeforeResolveReferences"/>


===================================================
AfterResolveReferences
===================================================
<Target Name="AfterResolveReferences"/>


===================================================
AssignProjectConfiguration
Assigns the appropriate configuration to each project in the list of project references passed in.
Adds to the project references passed in any project references implied by dependencies expressed in the solution file, if any.
===================================================
<Target Name="AssignProjectConfiguration"
        Condition="'$(CurrentSolutionConfigurationContents)' != '' or '@(ProjectReference)'!=''">


===================================================
ResolveProjectReferences
Build referenced projects
===================================================
<Target Name="ResolveProjectReferences"
        DependsOnTargets="AssignProjectConfiguration;_SplitProjectReferencesByFileExistence"
        Returns="@(_ResolvedNativeProjectReferencePaths);@(_ResolvedProjectReferencePaths)">


===================================================
GetTargetPath
This stand-alone target returns the name of the build product (i.e. EXE, DLL)
that would be produced if we built this project.
===================================================
<Target Name="GetTargetPath"
        DependsOnTargets="$(GetTargetPathDependsOn)"
        Returns="$(TargetPath)"/>


===================================================
GetTargetPathWithTargetPlatformMoniker
This stand-alone target returns the name and version of the target platform for this project.
===================================================
<Target Name="GetTargetPathWithTargetPlatformMoniker"
        DependsOnTargets="$(GetTargetPathWithTargetPlatformMonikerDependsOn)"
        Returns="@(TargetPathWithTargetPlatformMoniker)">


===================================================
GetNativeManifest
Compute the manifest item for this project.
===================================================
<Target
        Name="GetNativeManifest"
        Returns="@(ComputedApplicationManifest)">


===================================================
ResolveNativeReferences
Resolve native references
===================================================
<Target Name="ResolveNativeReferences"
        Condition="'@(NativeReference)'!=''"
        DependsOnTargets="ResolveProjectReferences">


===================================================
ResolveAssemblyReferences
Given the list of assemblies, find the closure of all assemblies that they depend on. These are
what we need to copy to the output directory.

[IN]
@(Reference) - List of assembly references as fusion names.
@(_ResolvedProjectReferencePaths) - List of project references produced by projects that this project depends on.

        The 'Private' attribute on the reference corresponds to the Copy Local flag in IDE.
        The 'Private' flag can have three possible values:
                - 'True' means the reference should be Copied Local
                - 'False' means the reference should not be Copied Local
                - [Missing] means this task will decide whether to treat this reference as CopyLocal or not.

[OUT]
@(ReferencePath) - Paths to resolved primary files.
@(ReferenceDependencyPaths) - Paths to resolved dependency files.
@(_ReferenceRelatedPaths) - Paths to .xmls and .pdbs.
@(ReferenceSatellitePaths) - Paths to satellites.
@(_ReferenceSerializationAssemblyPaths) - Paths to XML serialization assemblies created by sgen.
@(_ReferenceScatterPaths) - Paths to scatter files.
@(ReferenceCopyLocalPaths) - Paths to files that should be copied to the local directory.
===================================================
<Target Name="ResolveAssemblyReferences"
        Returns="@(ReferencePath)"
        DependsOnTargets="$(ResolveAssemblyReferencesDependsOn)">


===================================================
GenerateBindingRedirects
Inject the binding redirects into the app config file based on suggested redirects as output from ResolveAssemblyReferences.

[IN]
@(AppConfigWithTargetPath) - Path to the source app config file. This can be null if the project 
                                                        doesn't contain an app config file.
$(TargetFileName) -          The file name of the build target.

[OUT]
@(OutputAppConfigFile) -     Path to the output app config file in the intermediate directory.
===================================================
<Target Name="GenerateBindingRedirects"
        Inputs="$(MSBuildAllProjects);@(AppConfigFile);$(ResolveAssemblyReferencesStateFile);$(IntermediateOutputPath);@(SuggestedBindingRedirects)"
        Outputs="$(_GenerateBindingRedirectsIntermediateAppConfig)"
        Condition="'$(AutoGenerateBindingRedirects)' == 'true' and '$(GenerateBindingRedirectsOutputType)' == 'true'">


===================================================
GenerateBindingRedirectsUpdateAppConfig
Updates the project to use the generated app.config content.  This needs to run regardless of 
inputs/outputs so it is separate from GenerateBindingRedirects.
===================================================
<Target Name="GenerateBindingRedirectsUpdateAppConfig"
        AfterTargets="GenerateBindingRedirects"
        Condition="'$(AutoGenerateBindingRedirects)' == 'true' and '$(GenerateBindingRedirectsOutputType)' == 'true' and Exists('$(_GenerateBindingRedirectsIntermediateAppConfig)')">


===================================================
GetInstalledSDKs
Gets the list of SDKs installed in the SDKDirectoryRoot and SDKRegistryRoot locations
These paths are used by the ResolveSDKReference task and the ResolveAssemblyReference task.
===================================================
<Target Name="GetInstalledSDKLocations"
      DependsOnTargets="$(GetInstalledSDKLocationsDependsOn)"
      Returns="@(InstalledSDKLocations)" />


===================================================
ResolveSDKReferences
Given a list of SDKReference items and a list of resolved winmd files which may contain metadata as to which sdk they came from
we need to find the sdk root folders on disk and populate a ResolvedSDKReference item which has the full path to the SDK ROOT 
and the sdk identity as a piece of metadata.
===================================================
<Target Name="ResolveSDKReferences"
        Returns="@(ResolvedSDKReference)"
        DependsOnTargets="$(ResolveSDKReferencesDependsOn)">


===================================================
FindInvalidProjectReferences
Find project to project references with target platform version higher than the one used by the current project and 
creates a list of invalid references to be unresolved. It issues a warning for each invalid reference.
===================================================
<Target Name="FindInvalidProjectReferences"
        Condition ="'$(FindInvalidProjectReferences)' == 'true'"
        DependsOnTargets="$(FindInvalidProjectReferencesDependsOn)">


===================================================
ExpandSDKReferences
After we have resolved the sdk refrence we need to make sure that we automatically include the references which are part of the SDK (both winmd and dll)
as part of the assemblies passed to the compiler.

Project systems or project which do not want to reference all dlls or winmd files should override this target to do nothing.
===================================================
<Target Name="ExpandSDKReferences"
        Returns="@(ReferencesFromSDK)"
        DependsOnTargets="$(ExpandSDKReferencesDependsOn)" />


===================================================
ExportWindowsMDFile
When a project is generating a a winmd file through c# or vb, ect the compiler will create a WinMDModule file. This file needs to be run
through the winmdexp tool in order to generate the resulting WinMD file.
===================================================
<Target Name="ExportWindowsMDFile"
        DependsOnTargets="Compile"
        Condition="'$(ExportWinMDFile)' == 'true'"
        Inputs="@(IntermediateAssembly);@(DocFileItem);@(_DebugSymbolsIntermediatePath);@(ReferencePath);$(MSBuildAllProjects)"
        Outputs="$(_IntermediateWindowsMetadataPath);$(WinMDExpOutputPdb);$(WinMDOutputDocumentationFile)" />


===================================================
DesignTimeResolveAssemblyReferences
Given the list of assemblies, resolve their reference paths.
This target is called by Visual Studio at run time in order to filter references
according to the targeted framework.
===================================================
<Target Name="DesignTimeResolveAssemblyReferences"
        Condition="'$(DesignTimeReference)'!=''"
        DependsOnTargets="$(DesignTimeResolveAssemblyReferencesDependsOn)">


===================================================
ResolveComReferences
Resolve COM references
===================================================
<Target Name="ResolveComReferences"
        Condition="'@(COMReference)'!='' or '@(COMFileReference)'!=''"
        Returns="@(ReferencePath)"
        DependsOnTargets="PrepareForBuild;ResolveKeySource;ResolveAssemblyReferences" />


===================================================
PrepareResources
Prepare resources for the Compile step.
===================================================
<Target Name="PrepareResources"
        DependsOnTargets="$(PrepareResourcesDependsOn)"/>


===================================================
PrepareResourceNames
Prepare the names of resource files.
===================================================
<Target Name="PrepareResourceNames"
        DependsOnTargets="$(PrepareResourceNamesDependsOn)"/>


===================================================
AssignTargetPaths
This target creates <TargetPath> tags for items. <TargetPath> is a relative folder plus filename
for the destination of this item.
===================================================
<Target Name="AssignTargetPaths"
        DependsOnTargets="$(AssignTargetPathsDependsOn)">


===================================================
GetItemTargetPaths
This target returns all items that have TargetPath metadata assigned by the AssignTargetPaths target.
===================================================
<Target Name="GetItemTargetPaths"
        DependsOnTargets="AssignTargetPaths"
        Returns="
        @(EmbeddedResource);
        @(ContentWithTargetPath);
        @(_NoneWithTargetPath);
        @(_DeploymentBaseManifestWithTargetPath);
        " />


===================================================
SplitResourcesByCulture
Split EmbeddedResource items into five lists based on whether
they are resx files, licx files or other resources and whether they should be localized. Also adds Type and Culture
metadata. Type indicates whether the resource is "Resx" or "Non-Resx".
===================================================
<Target Name="SplitResourcesByCulture"
        DependsOnTargets="AssignTargetPaths">


===================================================
CreateCustomManifestResourceNames
Allows custom manifest resource name generation tasks to plug
into the build process
===================================================
<Target Name="CreateCustomManifestResourceNames"
        DependsOnTargets="$(CreateCustomManifestResourceNamesDependsOn)"/>


===================================================
ResGen
Run GenerateResource on the given resx files.
===================================================
<Target Name="ResGen"
        DependsOnTargets="$(ResGenDependsOn)"/>


===================================================
BeforeResGen
===================================================
<Target Name="BeforeResGen"/>


===================================================
AfterResGen
===================================================
<Target Name="AfterResGen"/>


===================================================
ResolveKeySource
Resolve the strong name key used to sign the assembly as well as the certificate used to
sign the ClickOnce manifests.
===================================================
<Target Name="ResolveKeySource"
        Condition="$(SignManifests) == 'true' or $(SignAssembly) == 'true'">


===================================================
Compile
===================================================
<Target Name="Compile"
        DependsOnTargets="$(CompileDependsOn)"/>


===================================================
GenerateTargetFrameworkMonikerAttribute
Emit the target framework moniker attribute as  a code fragment into a temporary source file for the compiler.
===================================================
<Target Name="GenerateTargetFrameworkMonikerAttribute"
        BeforeTargets="BeforeCompile"
        DependsOnTargets="PrepareForBuild;GetReferenceAssemblyPaths"
        Inputs="$(MSBuildToolsPath)\Microsoft.Common.targets"
        Outputs="$(TargetFrameworkMonikerAssemblyAttributesPath)"
        Condition="'$(GenerateTargetFrameworkAttribute)' == 'true'">


===================================================
GenerateAdditionalSources
Emit any specified code fragments into a temporary source file for the compiler.
===================================================
<Target Name="GenerateAdditionalSources"
        BeforeTargets="BeforeCompile"
        DependsOnTargets="PrepareForBuild;GetReferenceAssemblyPaths"
        Inputs="$(MSBuildAllProjects)"
        Outputs="$(AssemblyAttributesPath)"
        Condition="'@(AssemblyAttributes)' != '' and '$(GenerateAdditionalSources)' == 'true'">


===================================================
BeforeCompile
===================================================
<Target Name="BeforeCompile"/>


===================================================
AfterCompile
===================================================
<Target Name="AfterCompile"/>


===================================================
GenerateSerializationAssemblies
Run GenerateSerializationAssemblies on the assembly produced by this build.
===================================================
<Target Name="GenerateSerializationAssemblies"
        Condition="'$(_SGenGenerateSerializationAssembliesConfig)' == 'On' or ('@(WebReferenceUrl)'!='' and '$(_SGenGenerateSerializationAssembliesConfig)' == 'Auto')"
        DependsOnTargets="AssignTargetPaths;Compile;ResolveKeySource"
        Inputs="$(MSBuildAllProjects);@(IntermediateAssembly)"
        Outputs="$(IntermediateOutputPath)$(_SGenDllName)">


===================================================
CreateSatelliteAssemblies
Create one satellite assembly for every unique culture in the resources.
===================================================
<Target Name="CreateSatelliteAssemblies"
        DependsOnTargets="$(CreateSatelliteAssembliesDependsOn)" />


===================================================
GenerateSatelliteAssemblies
Actually run al.exe to create the satellite assemblies.
===================================================
<Target Name="GenerateSatelliteAssemblies"
        Inputs="$(MSBuildAllProjects);@(_SatelliteAssemblyResourceInputs);$(IntermediateOutputPath)$(TargetName)$(TargetExt)"
        Outputs="$(IntermediateOutputPath)%(Culture)\$(TargetName).resources.dll"
        Condition="'@(_SatelliteAssemblyResourceInputs)' != ''">


===================================================
ComputeIntermediateSatelliteAssemblies
Compute the paths to the intermediate satellite assemblies,
with culture attributes so we can copy them to the right place.
===================================================
<Target Name="ComputeIntermediateSatelliteAssemblies"
        Condition="@(EmbeddedResource->'%(WithCulture)') != ''"
        DependsOnTargets="$(ComputeIntermediateSatelliteAssembliesDependsOn)">


===================================================
SetWin32ManifestProperties
Set Win32Manifest and EmbeddedManifest properties to be used later in the build.
===================================================
<Target Name="SetWin32ManifestProperties"
        Condition="'$(Win32Manifest)'==''"
        DependsOnTargets="ResolveComReferences;ResolveNativeReferences;_SetExternalWin32ManifestProperties;_SetEmbeddedWin32ManifestProperties" />


===================================================
GenerateManifests
Generates ClickOnce application and deployment manifests or a native manifest.
===================================================
<Target Name="GenerateManifests"
        Condition="'$(GenerateClickOnceManifests)'=='true' or '@(NativeReference)'!='' or '@(ResolvedIsolatedComModules)'!='' or '$(GenerateAppxManifest)' == 'true'"
        DependsOnTargets="$(GenerateManifestsDependsOn)"/>


===================================================
GenerateApplicationManifest
Generates a ClickOnce or native application manifest.
An application manifest specifies declarative application identity, dependency and security information.
===================================================
<Target Name="GenerateApplicationManifest"
        DependsOnTargets="
                _DeploymentComputeNativeManifestInfo;
                _DeploymentComputeClickOnceManifestInfo;
                ResolveComReferences;
                ResolveNativeReferences;
                _GenerateResolvedDeploymentManifestEntryPoint"
        Inputs="
                $(MSBuildAllProjects);
                @(AppConfigWithTargetPath);
                $(_DeploymentBaseManifest);
                @(ResolvedIsolatedComModules);
                @(_DeploymentManifestDependencies);
                @(_DeploymentResolvedManifestEntryPoint);
                @(_DeploymentManifestFiles)"
        Outputs="@(ApplicationManifest)">


===================================================
GenerateDeploymentManifest
Generates a ClickOnce deployment manifest.
An deployment manifest specifies declarative application identity and application update information.
===================================================
<Target Name="GenerateDeploymentManifest"
        DependsOnTargets="GenerateApplicationManifest"
        Inputs="
                $(MSBuildAllProjects);
                @(ApplicationManifest)
                "
        Outputs="@(DeployManifest)">


===================================================
PrepareForRun
Copy the build outputs to the final directory if they have changed.
===================================================
<Target Name="PrepareForRun"
        DependsOnTargets="$(PrepareForRunDependsOn)"/>


===================================================
CopyFilesToOutputDirectory
Copy all build outputs, satellites and other necessary files to the final directory.
===================================================
<Target Name="CopyFilesToOutputDirectory"
        DependsOnTargets="
                ComputeIntermediateSatelliteAssemblies;
                _CopyFilesMarkedCopyLocal;
                _CopySourceItemsToOutputDirectory;
                _CopyAppConfigFile;
                _CopyManifestFiles;
                _CheckForCompileOutputs;
                _SGenCheckForOutputs">


===================================================
GetCopyToOutputDirectoryItems
Get all project items that may need to be transferred to the output directory.
This includes baggage items from transitively referenced projects. It would appear
that this target computes full transitive closure of content items for all referenced
projects; however that is not the case. It only collects the content items from its
immediate children and not children of children. The reason this happens is that
the ProjectReferenceWithConfiguration list that is consumed by _SplitProjectReferencesByFileExistence
is only populated in the current project and is empty in the children. The empty list
causes _MSBuildProjectReferenceExistent to be empty and terminates the recursion.
===================================================
<Target Name="GetCopyToOutputDirectoryItems"
        Returns="@(AllItemsFullPathWithTargetPath)"
        KeepDuplicateOutputs=" '$(MSBuildDisableGetCopyToOutputDirectoryItemsOptimization)' == '' "
        DependsOnTargets="$(GetCopyToOutputDirectoryItemsDependsOn)">


===================================================
UnmanagedRegistration
Registers the main assembly for COM interop.
===================================================
<Target Name="UnmanagedRegistration"
        Condition="'$(RegisterForComInterop)'=='true' and '$(OutputType)'=='library'"
        DependsOnTargets="$(UnmanagedRegistrationDependsOn)" />>


===================================================
IncrementalClean
Remove files that were produced in a prior build but weren't produced in the current build.
The reason is that if, for example, the name of the .exe has changed we want to delete the
old copy.

Leave the Clean cache file containing only the files produced in the current build.
===================================================
<Target Name="IncrementalClean"
        DependsOnTargets="_CleanGetCurrentAndPriorFileWrites">


===================================================
Clean
Delete all intermediate and final build outputs.
===================================================
<Target Name="Clean"
        Condition=" '$(_InvalidConfigurationWarning)' != 'true' "
        DependsOnTargets="$(CleanDependsOn)" />


===================================================
BeforeClean
===================================================
<Target Name="BeforeClean"/>


===================================================
AfterClean
===================================================
<Target Name="AfterClean"/>


===================================================
CleanReferencedProjects
Call Clean target on all Referenced Projects.
===================================================
<Target Name="CleanReferencedProjects"
        DependsOnTargets="AssignProjectConfiguration; _SplitProjectReferencesByFileExistence">


===================================================
CleanPublishFolder
===================================================
<Target Name="CleanPublishFolder"/>


===================================================
PostBuildEvent
Run the post-build event. This step is driven by two parameters:

(1) The $(RunPostBuildEvent) property is set by the user through the IDE and can be one of four values.

        - OnBuildSuccess: In this case, every step of the build must succeed for the post-build step to run.
        - <Blank>: This is the same as OnBuildSuccess.
        - OnOutputUpdated: In this case, the post-build step will run only if the main output assembly was
        actually updated.
        - Always: The post-build step is always run.

(2) The $(_AssemblyTimestampBeforeCompile) and $(_AssemblyTimestampAfterCompile) values are
        set by the _TimeStampBeforeCompile and _TimeStampAfterCompile targets.  If the assembly was actually
        rebuilt during this build, then the two values will be different.
===================================================
<Target Name="PostBuildEvent"
        Condition="'$(PostBuildEvent)' != '' and ('$(RunPostBuildEvent)' != 'OnOutputUpdated' or '$(_AssemblyTimestampBeforeCompile)' != '$(_AssemblyTimestampAfterCompile)')"
        DependsOnTargets="$(PostBuildEventDependsOn)">


===================================================
Publish
This target is only called when doing ClickOnce publishing outside the IDE, which implicitly builds before publishing.
===================================================
<Target Name="Publish"
        DependsOnTargets="$(PublishDependsOn)"/>


===================================================
SetGenerateManifests
This target simply assures the GenerateClickOnceManifests property is set whenever the publish target is invoked.
===================================================
<Target Name="SetGenerateManifests"/>


===================================================
PublishOnly
The "PublishOnly" target is intended for ClickOnce publishing inside the IDE, where the build has already been done
by the BuildManager.
===================================================
<Target Name="PublishOnly"
        DependsOnTargets="$(PublishOnlyDependsOn)"/>


===================================================
BeforePublish
===================================================
<Target Name="BeforePublish"/>


===================================================
AfterPublish
===================================================
<Target Name="AfterPublish"/>


===================================================
PublishBuild
Defines the set of targets that publishing is directly dependent on.
===================================================
<Target Name="PublishBuild"
        DependsOnTargets="$(PublishBuildDependsOn)"/>


===================================================
AllProjectOutputGroups
The targets below drive output groups, which provide generic information about a
project's inputs (e.g., content files, compilation sources, etc.) and built outputs
(e.g., built EXE/DLL, PDB, XML documentation files, etc.)

Each target may produce two kinds of items:  outputs and dependencies.  Outputs are
items from the current project; dependencies are items that are brought into the
current project as a result of referencing other projects or components.

For both outputs and dependencies, the Include attribute
specifies the location of the output/dependency; it must be a full path.  Any number
of additional attributes may be placed on an output/dependency item.
===================================================
<Target Name="AllProjectOutputGroups"
        DependsOnTargets="
                BuiltProjectOutputGroup;
                DebugSymbolsProjectOutputGroup;
                DocumentationProjectOutputGroup;
                SatelliteDllsProjectOutputGroup;
                SourceFilesProjectOutputGroup;
                ContentFilesProjectOutputGroup;
                SGenFilesOutputGroup"/>


===================================================
BuiltProjectOutputGroup
This target performs population of the Build project output group.
===================================================
<Target Name="BuiltProjectOutputGroup"
        Returns="@(BuiltProjectOutputGroupOutput)"
        DependsOnTargets="$(BuiltProjectOutputGroupDependsOn)">


===================================================
DebugSymbolsProjectOutputGroup
This target performs population of the Debug Symbols project output group.
===================================================
<Target Name="DebugSymbolsProjectOutputGroup"
        Returns="@(DebugSymbolsProjectOutputGroupOutput)"
        DependsOnTargets="$(DebugSymbolsProjectOutputGroupDependsOn)"/>


===================================================
DocumentationProjectOutputGroup
This target performs population of the Documentation project output group.
===================================================
<Target Name="DocumentationProjectOutputGroup"
        Returns="@(DocumentationProjectOutputGroupOutput)"
        DependsOnTargets="$(DocumentationProjectOutputGroupDependsOn)"/>


===================================================
SatelliteDllsProjectOutputGroup
This target performs population of the Satellite Files project output group.
===================================================
<Target Name="SatelliteDllsProjectOutputGroup"
        Returns="@(SatelliteDllsProjectOutputGroupOutput)"
        DependsOnTargets="$(SatelliteDllsProjectOutputGroupDependsOn)">


===================================================
SourceFilesProjectOutputGroup
This target performs population of the Source Files project output group.
Source files are items in the project whose type is "Compile" and "EmbeddedResource".
===================================================
<Target Name="SourceFilesProjectOutputGroup"
        Returns="@(SourceFilesProjectOutputGroupOutput)"
        DependsOnTargets="$(SourceFilesProjectOutputGroupDependsOn)">


===================================================
ContentFilesProjectOutputGroup
This target performs population of the Content Files project output group.
Content files are items in the project whose type is "Content".
===================================================
<Target Name="ContentFilesProjectOutputGroup"
        Returns="@(ContentFilesProjectOutputGroupOutput)"
        DependsOnTargets="$(ContentFilesProjectOutputGroupDependsOn)">


===================================================
SGenFilesOutputGroup
This target performs population of the GenerateSerializationAssemblies Files project output group.
GenerateSerializationAssemblies files are those generated by the GenerateSerializationAssemblies target and task.
===================================================
<Target Name="SGenFilesOutputGroup"
        Returns="@(SGenFilesOutputGroupOutput)"
        DependsOnTargets="$(SGenFilesOutputGroupDependsOn)"/>


===================================================
GetResolvedSDKReferences
These targets are to gather information from the SDKs.
===================================================
<Target Name="GetResolvedSDKReferences"
        DependsOnTargets="ResolveSDKReferences"
        Returns="@(ResolvedSDKReference)"/>


===================================================
PriFilesOutputGroup
This target performs population of the pri files output group
===================================================
<Target Name="PriFilesOutputGroup"
        Condition="'@(_ReferenceRelatedPaths)' != ''"
        DependsOnTargets="BuildOnlySettings;PrepareForBuild;AssignTargetPaths;ResolveReferences"
        Returns="@(PriFilesOutputGroupOutput)">


===================================================
SDKRedistOutputGroup
This target gathers the Redist folders from the SDKs which have been resolved.
===================================================
<Target Name="SDKRedistOutputGroup"
        Returns="@(SDKRedistOutputGroupOutput)"
        DependsOnTargets="$(SDKRedistOutputGroupDependsOn)"/>
```

## <a name="see-also"></a>関連項目

- [MSBuild の概念](../msbuild/msbuild-concepts.md)
- [方法: 複数のプロジェクト ファイルで同じターゲットを使用する](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)
