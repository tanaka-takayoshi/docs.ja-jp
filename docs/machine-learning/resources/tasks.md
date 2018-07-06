---
title: 機械学習のタスク
description: ML.NET でサポートされる機械学習のさまざまなタスクについて説明します。
ms.date: 06/04/2018
author: aditidugar
ms.author: johalex
ms.openlocfilehash: 875006a9cddb87b5f9436b78773420858fd842dd
ms.sourcegitcommit: 6bc4efca63e526ce6f2d257fa870f01f8c459ae4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2018
ms.locfileid: "36207727"
---
# <a name="machine-learning-tasks"></a>機械学習のタスク

機械学習モデルを構築する場合は、データを使用して実現したい目的を最初に定義する必要があります。 その後で、状況に適した機械学習のタスクを選択できます。 選択可能な機械学習のさまざまなタスクといくつかの一般的なユース ケースについて以下で説明します。 

> [!NOTE]
> ML.NET は現在プレビュー段階です。 現時点では、機械学習のタスクがすべてサポートされているわけではありません。 特定のタスクに対するご要望を送信するには、[dotnet/machinelearning リポジトリ](https://github.com/dotnet/machinelearning/issues)で問題をオープンしてください。

> [!NOTE]
> 現時点で、ML.NET は画像を使用する機械学習のタスクをサポートしていません。 このサポートは今後のリリースで追加される予定です。 

## <a name="binary-classification"></a>二項分類

データのインスタンスが 2 つのうちのどちらのクラス (カテゴリ) に属しているかを予測するために使用する[教師あり機械学習](glossary.md#supervised-machine-learning)タスクです。 分類アルゴリズムの入力はラベル付けされた一連のサンプルであり、各ラベルは整数 0 または 1 です。 二項分類アルゴリズムの出力は分類子であり、ラベルのない新しいインスタンスのクラスを予測するために使用できます。 二項分類のシナリオの例を次に示します。

* [Twitter コメントのセンチメントが "肯定的" か "否定的" かを理解する](../tutorials/sentiment-analysis.md)。
* 患者が特定の病気であるかどうかを診断する。
* 電子メールを "スパム" としてマークするかどうかを決定する。

詳しくは、Wikipedia の[二項分類](https://en.wikipedia.org/wiki/Binary_classification)の記事を参照してください。

## <a name="multiclass-classification"></a>多クラス分類

データのインスタンスのクラス (カテゴリ) を予測するために使用する[教師あり機械学習](glossary.md#supervised-machine-learning)タスクです。 分類アルゴリズムの入力は、ラベル付けされた一連のサンプルです。 各ラベルは 0 ～ k-1 の整数であり、k はクラスの数です。 分類アルゴリズムの出力は分類子であり、ラベルのない新しいインスタンスのクラスを予測するために使用できます。 多クラス分類のシナリオの例を次に示します。

* "シベリアン ハスキー"、"ゴールデン レトリバー"、"プードル" などの犬種を特定する。
* 映画のレビューが "肯定的"、"中立"、"否定的" のどれかを理解する。
* ホテルのレビューを "立地"、"価格"、"清潔さ" などに分類する。

詳しくは、Wikipedia の[多クラス分類](https://en.wikipedia.org/wiki/Multiclass_classification)の記事を参照してください。

## <a name="regression"></a>回帰

関連する一連の特徴からラベルの値を予測するために使用する[教師あり機械学習](glossary.md#supervised-machine-learning)タスクです。 ラベルには任意の実際の値を使用できます。分類タスクのように有限の値のセットから取得するものではありません。 回帰アルゴリズムでは、ラベルに関連する特徴におけるラベルの依存関係をモデル化して、特徴の値が変化するとラベルがどのように変化するかを判断します。 回帰アルゴリズムの入力は、既知の値のラベルが付いた一連のサンプルです。 回帰アルゴリズムの出力は関数であり、新しい入力特徴のセットのラベル値を予測するために使用できます。 回帰のシナリオの例を次に示します。

* 住宅の属性 (寝室数、立地、規模など) に基づいて住宅価格を予測する。
* 履歴データと現在の市場動向に基づいて将来の株価を予測する。
* 広告予算に基づいて製品の売り上げを予測する。

> [!NOTE]
> 現在、ML.NET では時系列を含む回帰タスクのサポートを構築中です。

## <a name="clustering"></a>クラスタリング

データのインスタンスを、同様の特性を持つクラスタにグループ化するために使用する[教師なし機械学習](glossary.md#unsupervised-machine-learning)タスクです。 また、閲覧や単純な観測では論理的に導き出せない可能性のあるデータ セットにおける関係をクラスタリングを使用して識別することもできます。 クラスタリング アルゴリズムの入力と出力は、選択した方法によって異なります。 分布、重心、結合性、または密度に基づくアプローチを利用できます。 現在、ML.NET では、K 平均法によるクラスタリングを使用した重心に基づくアプローチをサポートしています。 クラスタリングのシナリオの例を次に示します。

* ホテル選択の傾向と特性に基づいてホテルの宿泊客のセグメントを理解する。
* 対象を絞った広告キャンペーンの構築に役立つ顧客セグメントと統計データを特定する。
* 製造メトリックに基づいてインベントリを分類する。

## <a name="anomaly-detection-coming-soon"></a>異常検知 (*準備中*)

## <a name="ranking-coming-soon"></a>ランク付け (*準備中*)

## <a name="recommendation-coming-soon"></a>推奨 (*準備中*)
