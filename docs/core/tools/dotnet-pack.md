---
title: "dotnet-pack コマンド | .NET Core SDK"
description: "dotnet-pack コマンドでは、.NET Core プロジェクトの NuGet パッケージを作成します。"
keywords: "dotnet-pack, CLI, CLI コマンド, .NET Core"
author: mairaw
manager: wpickett
ms.date: 10/12/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 8b4b8cef-f56c-4a10-aa01-fde8bfaae53e
translationtype: Human Translation
ms.sourcegitcommit: c6ee3f5663d0a3f62914e8de474cca4d15340c9d
ms.openlocfilehash: e83c8ad302590bcd77129c3ff325e498da751e69

---

#<a name="dotnetpack"></a>dotnet-pack

## <a name="name"></a>Name

`dotnet-pack`- NuGet パッケージにコードをパックします。

## <a name="synopsis"></a>構文

`dotnet pack [--help] [--output]  
    [--no-build] [--build-base-path]  
    [--configuration]  [--version-suffix]
    [project]`  

## <a name="description"></a>説明

`dotnet pack` コマンドはプロジェクトをビルドし、NuGet パッケージを作成します。 この操作の結果として、拡張子が `nupkg` の 2 つのパッケージが生成されます。 1 つのパッケージにコードが含まれ、もう 1 つにはデバッグ シンボルが含まれます。 

パックされるプロジェクトの NuGet 依存関係が nuspec ファイルに追加されるため、パッケージのインストール時に解決できます。 プロジェクト間参照はプロジェクト内にはパッケージ化されません。 現時点では、プロジェクト間の依存関係がある場合は、プロジェクトごとにパッケージが必要になります。

`dotnet pack`では、既定で最初にプロジェクトがビルドされます。 これを避けたい場合は、`--no-build` オプションを渡します。 これは、コードが既にビルドされていることがわかっている場合などの継続的インテグレーション (CI) ビルド シナリオで役立ちます。 

## <a name="options"></a>オプション

`-h|--help`

コマンドの短いヘルプを印刷します。  

`[project]` 
    
パックするプロジェクトです。 [project.json](project-json.md) ファイルまたはディレクトリのパスを指定できます。 省略すると、既定で現在のディレクトリに設定されます。 

`-o|--output <OUTPUT_DIRECTORY>`

指定したディレクトリにビルド済みパッケージを配置します。 

`--no-build`

パッキングの前にプロジェクトをビルドしません。 

`--build-base-path`

指定したディレクトリに一時的なビルド成果物を配置します。 既定では、現在のディレクトリの `obj` ディレクトリに配置されます。 

`-c|--configuration <Debug|Release>`

プロジェクトのビルド時に使用する構成です。 指定しない場合、既定で `Debug` に設定されます。

`--version-suffix`

指定された文字列で `-*` パッケージ バージョン サフィックスのアスタリスクを更新します。

## <a name="examples"></a>例

現在のディレクトリのプロジェクトをパックします。

`dotnet pack`

app1 プロジェクトをパックします。

`dotnet pack ~/projects/app1/project.json`
    
プロジェクトを現在のディレクトリにパックし、指定したフォルダーに生成されたパッケージを配置します。

`dotnet pack --output nupkgs`

現在のディレクトリのプロジェクトを指定したフォルダーにパックし、ビルド ステップをスキップします。

`dotnet pack --no-build --output nupkgs`

現在のプロジェクトをパックし、結果のパッケージ バージョンを指定されたサフィックスで更新します。 たとえば、バージョン `1.0.0-*` は `1.0.0-ci-1234` に更新されます。

`dotnet pack --version-suffix "ci-1234"`


<!--HONumber=Nov16_HO1-->


