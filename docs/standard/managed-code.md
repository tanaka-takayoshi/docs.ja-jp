---
title: "&quot;マネージ コード&quot; とは"
description: "&quot;マネージ コード&quot; とは"
keywords: .NET, .NET Core
author: blackdwarf
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 20bb7ea8-192e-4a96-8ef3-e10e1950fd3d
translationtype: Human Translation
ms.sourcegitcommit: 0013cf5604bfd1e8a16e5ca15577ac81fce49612
ms.openlocfilehash: 905c3706717a03f468e3dd5717c049e83f211e67

---

# <a name="what-is-managed-code"></a>"マネージ コード" とは

.NET Framework を使用していると、よく "マネージ コード" という用語を目にすることがあります。 このドキュメントでは、この用語の意味とそれに関する追加の情報について説明します。

ごく簡単に言うと、マネージ コードとは、その実行がランタイムによって管理されるコードです。 この場合、問題のランタイムは、実装 ([Mono](http://www.mono-project.com/) または .NET Framework または .NET Core) に関係なく、**共通言語ランタイム**または CLR と呼ばれます。 CLR は、マネージ コードの取得、そのマシン コードへのコンパイルと実行を担当します。 それに加えて、ランタイムは、自動メモリ管理、セキュリティ境界、タイプ セーフなどのいくつかの重要なサービスも提供します。

これを、"アンマネージ コード" とも呼ばれる C/C++ プログラムを実行する方法と比較します。 アンマネージ環境では、プログラマがほとんどすべてのことを担当します。 実際のプログラムは、基本的に、オペレーティング システム (OS) がメモリに読み込み、起動するバイナリです。 メモリ管理からセキュリティの考慮事項まで、他のすべてのことをプログラマが担当します。

マネージ コードは C#、Visual Basic、F# など、.NET プラットフォーム上で実行可能な高水準言語のいずれかで記述されます。 それらの言語で書かれたコードをそれぞれのコンパイラでコンパイルした場合、マシン コードは得られません。 **中間言語**コードが得られ、それをランタイムがコンパイルして実行します。 C++ は、Windows で実行するネイティブなアンマネージ バイナリも生成できるため、この規則の 1 つの例外です。

## <a name="intermediate-language-execution"></a>中間言語と実行

"中間言語" (または略して IL) とは それは、高水準 .NET 言語で記述されたコードのコンパイルの成果物です。 これらの言語のいずれかで記述されたコードをコンパイルすると、IL で構成されたバイナリが得られます。 IL はランタイムで実行される特定の言語に依存しないことに注意してください。それについて個別の仕様もあるため、参照することができます。

高水準コードから IL を生成したら、ほとんどの場合、それを実行したいと考えるでしょう。 ここで、CLR が引き継ぎ、コードを IL から、CPU で実際に実行できるマシン コードに **Just-In-Time** コンパイル、つまり **JIT 処理**するプロセスを開始します。 このように、CLR はコードが実行することを正確にわかっているため、それを効率的に_管理_できます。

中間言語は、共通中間言語 (CIL) または Microsoft Intermediate Language (MSIL) と呼ばれることもあります。

## <a name="unmanaged-code-interoperability"></a>アンマネージ コードの相互運用性

もちろん、CLR は、マネージ環境とアンマネージ環境間の境界を越えることができ、[基本クラス ライブラリ](framework-libraries.md)にも、それを行う多くのコードがあります。 これは**相互運用性 (interoperability) **または略して **相互運用 (interop)** と呼ばれます。 これらのプロビジョニングにより、たとえばアンマネージ ライブラリをラップし、それを呼び出すことができます。 ただし、これを実行すると、コードがランタイムの境界を越えたときに、実行の実際の管理が再びアンマネージ コードの担当になるため、同じ制限が課せられることになります。

これと同様に、C# は、実行が CLR によって管理されないコードの一部を指定する**アンセーフ コンテキスト**として知られる機能を使用して、コード内の直接のポインターなど、アンマネージ コンストラクトを使用できる 1 つの言語です。

## <a name="more-resources"></a>その他のリソース

*   [.NET framework の概念の概要](https://msdn.microsoft.com/library/zw4w595w.aspx)
*   [アンセーフ コードとポインター](https://msdn.microsoft.com/library/t2yzs44b.aspx)
*   [相互運用性 (C# プログラミング ガイド)](https://msdn.microsoft.com/library/ms173184.aspx)



<!--HONumber=Nov16_HO3-->


