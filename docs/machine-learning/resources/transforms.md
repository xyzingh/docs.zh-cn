---
title: 数据转换
description: 了解在 ML.NET 中受支持的特征工程组件。
ms.date: 04/02/2019
ms.openlocfilehash: ca410b475c556db5ad4c3862fb79755b455d6830
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92224214"
---
# <a name="data-transformations"></a><span data-ttu-id="62c13-103">数据转换</span><span class="sxs-lookup"><span data-stu-id="62c13-103">Data transformations</span></span>

<span data-ttu-id="62c13-104">数据转换用于：</span><span class="sxs-lookup"><span data-stu-id="62c13-104">Data transformations are used to:</span></span>

- <span data-ttu-id="62c13-105">准备用于模型训练的数据</span><span class="sxs-lookup"><span data-stu-id="62c13-105">prepare data for model training</span></span>
- <span data-ttu-id="62c13-106">采用 TensorFlow 或 ONNX 格式应用导入的模型</span><span class="sxs-lookup"><span data-stu-id="62c13-106">apply an imported model in TensorFlow or ONNX format</span></span>
- <span data-ttu-id="62c13-107">通过模型传递数据后对其进行后处理</span><span class="sxs-lookup"><span data-stu-id="62c13-107">post-process data after it has been passed through a model</span></span>

<span data-ttu-id="62c13-108">本指南中的数据转换返回实现 [IEstimator](xref:Microsoft.ML.IEstimator%601) 接口的类。</span><span class="sxs-lookup"><span data-stu-id="62c13-108">The transformations in this guide return classes that implement the [IEstimator](xref:Microsoft.ML.IEstimator%601) interface.</span></span> <span data-ttu-id="62c13-109">数据转换可以链接在一起。</span><span class="sxs-lookup"><span data-stu-id="62c13-109">Data transformations can be chained together.</span></span> <span data-ttu-id="62c13-110">每个数据转换都需要获取并生成特定类型和格式的数据，链接的参考文档中规定了具体类型和格式。</span><span class="sxs-lookup"><span data-stu-id="62c13-110">Each transformation both expects and produces data of specific types and formats, which are specified in the linked reference documentation.</span></span>

<span data-ttu-id="62c13-111">一些数据转换需要通过定型数据来计算参数。</span><span class="sxs-lookup"><span data-stu-id="62c13-111">Some data transformations require training data to calculate their parameters.</span></span> <span data-ttu-id="62c13-112">例如，<xref:Microsoft.ML.NormalizationCatalog.NormalizeMeanVariance%2A> 转换器计算 `Fit()` 操作期间定型数据的平均值和方差，并在 `Transform()` 操作中使用这些参数。</span><span class="sxs-lookup"><span data-stu-id="62c13-112">For example: the <xref:Microsoft.ML.NormalizationCatalog.NormalizeMeanVariance%2A> transformer calculates the mean and variance of the training data during the `Fit()` operation, and uses those parameters in the `Transform()` operation.</span></span>

<span data-ttu-id="62c13-113">另一些数据转换不需要定型数据。</span><span class="sxs-lookup"><span data-stu-id="62c13-113">Other data transformations don't require training data.</span></span> <span data-ttu-id="62c13-114">例如，<xref:Microsoft.ML.ImageEstimatorsCatalog.ConvertToGrayscale%2A> 转换可以执行 `Transform()` 操作，而无需在 `Fit()` 操作期间看到任何定型数据。</span><span class="sxs-lookup"><span data-stu-id="62c13-114">For example: the <xref:Microsoft.ML.ImageEstimatorsCatalog.ConvertToGrayscale%2A> transformation can perform the `Transform()` operation without having seen any training data during the `Fit()` operation.</span></span>

## <a name="column-mapping-and-grouping"></a><span data-ttu-id="62c13-115">列映射和分组</span><span class="sxs-lookup"><span data-stu-id="62c13-115">Column mapping and grouping</span></span>

| <span data-ttu-id="62c13-116">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-116">Transform</span></span> | <span data-ttu-id="62c13-117">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-117">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.TransformExtensionsCatalog.Concatenate%2A> | <span data-ttu-id="62c13-118">将一个或多个输入列连接到新输出列中</span><span class="sxs-lookup"><span data-stu-id="62c13-118">Concatenate one or more input columns into a new output column</span></span> |
| <xref:Microsoft.ML.TransformExtensionsCatalog.CopyColumns%2A> | <span data-ttu-id="62c13-119">复制和重命名一个或多个输入列</span><span class="sxs-lookup"><span data-stu-id="62c13-119">Copy and rename one or more input columns</span></span> |
| <xref:Microsoft.ML.TransformExtensionsCatalog.DropColumns%2A> | <span data-ttu-id="62c13-120">删除一个或多个输入列</span><span class="sxs-lookup"><span data-stu-id="62c13-120">Drop one or more input columns</span></span> |
| <xref:Microsoft.ML.TransformExtensionsCatalog.SelectColumns%2A> | <span data-ttu-id="62c13-121">选择一个或多个不包含输入数据的列</span><span class="sxs-lookup"><span data-stu-id="62c13-121">Select one or more columns to keep from the input data</span></span> |

## <a name="normalization-and-scaling"></a><span data-ttu-id="62c13-122">规范化和缩放</span><span class="sxs-lookup"><span data-stu-id="62c13-122">Normalization and scaling</span></span>

| <span data-ttu-id="62c13-123">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-123">Transform</span></span> | <span data-ttu-id="62c13-124">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-124">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeMeanVariance%2A> | <span data-ttu-id="62c13-125">减去（定型数据的）平均值，再除以（定型数据的）方差</span><span class="sxs-lookup"><span data-stu-id="62c13-125">Subtract the mean (of the training data) and divide by the variance (of the training data)</span></span> |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeLogMeanVariance%2A> | <span data-ttu-id="62c13-126">根据定型数据的对数进行规范化</span><span class="sxs-lookup"><span data-stu-id="62c13-126">Normalize based on the logarithm of the training data</span></span> |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeLpNorm%2A> | <span data-ttu-id="62c13-127">按 [lp 范数](https://en.wikipedia.org/wiki/Lp_space#The_p-norm_in_finite_dimensions)缩放输入向量，其中 p 为 1、2 或无穷大。</span><span class="sxs-lookup"><span data-stu-id="62c13-127">Scale input vectors by their [lp-norm](https://en.wikipedia.org/wiki/Lp_space#The_p-norm_in_finite_dimensions), where p is 1, 2 or infinity.</span></span> <span data-ttu-id="62c13-128">默认为 l2（欧几里得距离）范数</span><span class="sxs-lookup"><span data-stu-id="62c13-128">Defaults to the l2 (Euclidean distance) norm</span></span> |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeGlobalContrast%2A> | <span data-ttu-id="62c13-129">缩放行中的每个值，具体方法是减去行数据的平均值，除以（行数据的）标准差或 l2 范数，再乘以可配置的比例因子（默认值为 2）</span><span class="sxs-lookup"><span data-stu-id="62c13-129">Scale each value in a row by subtracting the mean of the row data and divide by either the standard deviation or l2-norm (of the row data), and multiply by a configurable scale factor (default 2)</span></span> |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeBinning%2A> | <span data-ttu-id="62c13-130">将输入值分配到箱索引，并除以箱数量，以生成介于 0 和 1 之间的浮点值。</span><span class="sxs-lookup"><span data-stu-id="62c13-130">Assign the input value to a bin index and divide by the number of bins to produce a float value between 0 and 1.</span></span> <span data-ttu-id="62c13-131">计算箱边界是为了在各个箱中均匀分布定型数据</span><span class="sxs-lookup"><span data-stu-id="62c13-131">The bin boundaries are calculated to evenly distribute the training data across bins</span></span> |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeSupervisedBinning%2A> | <span data-ttu-id="62c13-132">根据与标签列的相关性，将输入值分配到箱</span><span class="sxs-lookup"><span data-stu-id="62c13-132">Assign the input value to a bin based on its correlation with label column</span></span> |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeMinMax%2A> | <span data-ttu-id="62c13-133">按定型数据最小值和最大值的差值缩放输入</span><span class="sxs-lookup"><span data-stu-id="62c13-133">Scale the input by the difference between the minimum and maximum values in the training data</span></span> |

## <a name="conversions-between-data-types"></a><span data-ttu-id="62c13-134">数据类型转换</span><span class="sxs-lookup"><span data-stu-id="62c13-134">Conversions between data types</span></span>

| <span data-ttu-id="62c13-135">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-135">Transform</span></span> | <span data-ttu-id="62c13-136">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-136">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.ConvertType%2A> | <span data-ttu-id="62c13-137">将输入列的类型转换为新类型</span><span class="sxs-lookup"><span data-stu-id="62c13-137">Convert the type of an input column to a new type</span></span> |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValue%2A> | <span data-ttu-id="62c13-138">根据提供的映射字典将值映射到键（类别）</span><span class="sxs-lookup"><span data-stu-id="62c13-138">Map values to keys (categories) based on the supplied dictionary of mappings</span></span> |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValueToKey%2A> | <span data-ttu-id="62c13-139">通过从输入数据创建映射，将值映射到键（类别）</span><span class="sxs-lookup"><span data-stu-id="62c13-139">Map values to keys (categories) by creating the mapping from the input data</span></span> |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapKeyToValue%2A> | <span data-ttu-id="62c13-140">将键转换回原始值</span><span class="sxs-lookup"><span data-stu-id="62c13-140">Convert keys back to their original values</span></span> |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapKeyToVector%2A> | <span data-ttu-id="62c13-141">将键转换回原始值的向量</span><span class="sxs-lookup"><span data-stu-id="62c13-141">Convert keys back to vectors of original values</span></span> |
| <xref:Microsoft.ML.ConversionsCatalog.MapKeyToBinaryVector%2A> | <span data-ttu-id="62c13-142">将键转换回原始值的二元向量</span><span class="sxs-lookup"><span data-stu-id="62c13-142">Convert keys back to a binary vector of original values</span></span> |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.Hash%2A> | <span data-ttu-id="62c13-143">哈希处理输入列中的值</span><span class="sxs-lookup"><span data-stu-id="62c13-143">Hash the value in the input column</span></span> |

## <a name="text-transformations"></a><span data-ttu-id="62c13-144">文本转换</span><span class="sxs-lookup"><span data-stu-id="62c13-144">Text transformations</span></span>

| <span data-ttu-id="62c13-145">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-145">Transform</span></span> | <span data-ttu-id="62c13-146">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-146">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.TextCatalog.FeaturizeText%2A> | <span data-ttu-id="62c13-147">将文本列转换为规范化 ngram 和 char-gram 计数的浮点数组</span><span class="sxs-lookup"><span data-stu-id="62c13-147">Transform a text column into a float array of normalized ngrams and char-grams counts</span></span> |
| <xref:Microsoft.ML.TextCatalog.TokenizeIntoWords%2A> | <span data-ttu-id="62c13-148">将一个或多个文本列拆分为各个字词</span><span class="sxs-lookup"><span data-stu-id="62c13-148">Split one or more text columns into individual words</span></span> |
| <xref:Microsoft.ML.TextCatalog.TokenizeIntoCharactersAsKeys%2A> | <span data-ttu-id="62c13-149">将一个或多个文本列拆分为关于一组主题的各个字符浮点数</span><span class="sxs-lookup"><span data-stu-id="62c13-149">Split one or more text columns into individual characters floats over a set of topics</span></span> |
| <xref:Microsoft.ML.TextCatalog.NormalizeText%2A> | <span data-ttu-id="62c13-150">更改大小写、删除标注字符、标点符号和数字</span><span class="sxs-lookup"><span data-stu-id="62c13-150">Change case, remove diacritical marks, punctuation marks, and numbers</span></span> |
| <xref:Microsoft.ML.TextCatalog.ProduceNgrams%2A> | <span data-ttu-id="62c13-151">将文本列转换为一组 ngram 计数（连续单词的序列）</span><span class="sxs-lookup"><span data-stu-id="62c13-151">Transform text column into a bag of counts of ngrams (sequences of consecutive words)</span></span>|
| <xref:Microsoft.ML.TextCatalog.ProduceWordBags%2A> | <span data-ttu-id="62c13-152">将文本列转换为一组 ngram 向量计数</span><span class="sxs-lookup"><span data-stu-id="62c13-152">Transform text column into a bag of counts of ngrams vector</span></span> |
| <xref:Microsoft.ML.TextCatalog.ProduceHashedNgrams%2A> | <span data-ttu-id="62c13-153">将文本列转换为已哈希处理的 ngram 计数向量</span><span class="sxs-lookup"><span data-stu-id="62c13-153">Transform text column into a vector of hashed ngram counts</span></span> |
| <xref:Microsoft.ML.TextCatalog.ProduceHashedWordBags%2A> | <span data-ttu-id="62c13-154">将文本列转换为一组已哈希处理的 ngram 计数</span><span class="sxs-lookup"><span data-stu-id="62c13-154">Transform text column into a bag of hashed ngram counts</span></span> |
| <xref:Microsoft.ML.TextCatalog.RemoveDefaultStopWords%2A>  | <span data-ttu-id="62c13-155">从输入列中删除指定语言的默认停用词</span><span class="sxs-lookup"><span data-stu-id="62c13-155">Remove default stop words for the specified language from input columns</span></span> |
| <xref:Microsoft.ML.TextCatalog.RemoveStopWords%2A> | <span data-ttu-id="62c13-156">从输入列中删除指定的停用词</span><span class="sxs-lookup"><span data-stu-id="62c13-156">Removes specified stop words from input columns</span></span> |
| <xref:Microsoft.ML.TextCatalog.LatentDirichletAllocation%2A> | <span data-ttu-id="62c13-157">将文档（表示为浮点数向量）转换为关于一组主题的浮点数向量</span><span class="sxs-lookup"><span data-stu-id="62c13-157">Transform a document (represented as a vector of floats) into a vector of floats over a set of topics</span></span> |
| <xref:Microsoft.ML.TextCatalog.ApplyWordEmbedding%2A> | <span data-ttu-id="62c13-158">使用预定型模型将文本令牌向量转换为句向量</span><span class="sxs-lookup"><span data-stu-id="62c13-158">Convert vectors of text tokens into sentence vectors using a pre-trained model</span></span> |

## <a name="image-transformations"></a><span data-ttu-id="62c13-159">图像转换</span><span class="sxs-lookup"><span data-stu-id="62c13-159">Image transformations</span></span>

| <span data-ttu-id="62c13-160">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-160">Transform</span></span> | <span data-ttu-id="62c13-161">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-161">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.ConvertToGrayscale%2A> | <span data-ttu-id="62c13-162">将图像转换为灰度图像</span><span class="sxs-lookup"><span data-stu-id="62c13-162">Convert an image to grayscale</span></span> |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.ConvertToImage%2A> | <span data-ttu-id="62c13-163">将像素向量转换为 <xref:Microsoft.ML.Transforms.Image.ImageDataViewType></span><span class="sxs-lookup"><span data-stu-id="62c13-163">Convert a vector of pixels to <xref:Microsoft.ML.Transforms.Image.ImageDataViewType></span></span> |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.ExtractPixels%2A> | <span data-ttu-id="62c13-164">将输入图像中的像素转换为数字向量</span><span class="sxs-lookup"><span data-stu-id="62c13-164">Convert pixels from input image into a vector of numbers</span></span> |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.LoadImages%2A> | <span data-ttu-id="62c13-165">将图像从文件夹加载到内存中</span><span class="sxs-lookup"><span data-stu-id="62c13-165">Load images from a folder into memory</span></span> |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.ResizeImages%2A> | <span data-ttu-id="62c13-166">调整图像大小</span><span class="sxs-lookup"><span data-stu-id="62c13-166">Resize images</span></span> |
| <xref:Microsoft.ML.OnnxCatalog.DnnFeaturizeImage%2A> | <span data-ttu-id="62c13-167">应用预训练的深度神经网络 (DNN) 模型将输入图像转换为特征向量</span><span class="sxs-lookup"><span data-stu-id="62c13-167">Applies a pre-trained deep neural network (DNN) model to transform an input image into a feature vector</span></span> |

## <a name="categorical-data-transformations"></a><span data-ttu-id="62c13-168">分类数据转换</span><span class="sxs-lookup"><span data-stu-id="62c13-168">Categorical data transformations</span></span>

| <span data-ttu-id="62c13-169">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-169">Transform</span></span> | <span data-ttu-id="62c13-170">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-170">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.CategoricalCatalog.OneHotEncoding%2A> | <span data-ttu-id="62c13-171">将一个或多个文本列转换为[单热](https://en.wikipedia.org/wiki/One-hot)编码向量</span><span class="sxs-lookup"><span data-stu-id="62c13-171">Convert one or more text columns into [one-hot](https://en.wikipedia.org/wiki/One-hot) encoded vectors</span></span> |
| <xref:Microsoft.ML.CategoricalCatalog.OneHotHashEncoding%2A> | <span data-ttu-id="62c13-172">将一个或多个文本列转换为基于哈希的单热编码向量</span><span class="sxs-lookup"><span data-stu-id="62c13-172">Convert one or more text columns into hash-based one-hot encoded vectors</span></span> |

## <a name="time-series-data-transformations"></a><span data-ttu-id="62c13-173">时序数据转换</span><span class="sxs-lookup"><span data-stu-id="62c13-173">Time series data transformations</span></span>

| <span data-ttu-id="62c13-174">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-174">Transform</span></span> | <span data-ttu-id="62c13-175">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-175">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.TimeSeriesCatalog.DetectAnomalyBySrCnn%2A> | <span data-ttu-id="62c13-176">使用 Spectral Residual (SR) 算法检测输入时序数据中的异常</span><span class="sxs-lookup"><span data-stu-id="62c13-176">Detect anomalies in the input time series data using the Spectral Residual (SR) algorithm</span></span> |
| <xref:Microsoft.ML.TimeSeriesCatalog.DetectChangePointBySsa%2A> | <span data-ttu-id="62c13-177">使用奇异谱分析 (SSA) 检测时序数据中的更改点</span><span class="sxs-lookup"><span data-stu-id="62c13-177">Detect change points in time series data using singular spectrum analysis (SSA)</span></span> |
| <xref:Microsoft.ML.TimeSeriesCatalog.DetectIidChangePoint%2A> | <span data-ttu-id="62c13-178">使用自适应内核密度估计和鞅评分检测独立同分布 (IID) 的时序数据中的更改点</span><span class="sxs-lookup"><span data-stu-id="62c13-178">Detect change points in independent and identically distributed (IID) time series data using adaptive kernel density estimations and martingale scores</span></span> |
| <xref:Microsoft.ML.TimeSeriesCatalog.ForecastBySsa%2A> | <span data-ttu-id="62c13-179">使用奇异谱分析 (SSA) 预测时序数据</span><span class="sxs-lookup"><span data-stu-id="62c13-179">Forecast time series data using singular spectrum analysis (SSA)</span></span> |
| <xref:Microsoft.ML.TimeSeriesCatalog.DetectSpikeBySsa%2A> | <span data-ttu-id="62c13-180">使用奇异谱分析 (SSA) 检测时序数据中的峰值</span><span class="sxs-lookup"><span data-stu-id="62c13-180">Detect spikes in time series data using singular spectrum analysis (SSA)</span></span> |
| <xref:Microsoft.ML.TimeSeriesCatalog.DetectIidSpike%2A> | <span data-ttu-id="62c13-181">使用自适应内核密度估计和鞅评分检测独立同分布 (IID) 的时序数据中的峰值</span><span class="sxs-lookup"><span data-stu-id="62c13-181">Detect spikes in independent and identically distributed (IID) time series data using adaptive kernel density estimations and martingale scores</span></span> |

## <a name="missing-values"></a><span data-ttu-id="62c13-182">缺少值</span><span class="sxs-lookup"><span data-stu-id="62c13-182">Missing values</span></span>

| <span data-ttu-id="62c13-183">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-183">Transform</span></span> | <span data-ttu-id="62c13-184">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-184">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.ExtensionsCatalog.IndicateMissingValues%2A> | <span data-ttu-id="62c13-185">新建布尔输出列：如果输入列中缺少值，输出列的值为 true</span><span class="sxs-lookup"><span data-stu-id="62c13-185">Create a new boolean output column, the value of which is true when the value in the input column is missing</span></span> |
| <xref:Microsoft.ML.ExtensionsCatalog.ReplaceMissingValues%2A> | <span data-ttu-id="62c13-186">新建输出列：如果输入列中缺少值，输出列的值设置为默认值，否则设置为输入值</span><span class="sxs-lookup"><span data-stu-id="62c13-186">Create a new output column, the value of which is set to a default value if the value is missing from the input column, and the input value otherwise</span></span> |

## <a name="feature-selection"></a><span data-ttu-id="62c13-187">功能选择</span><span class="sxs-lookup"><span data-stu-id="62c13-187">Feature selection</span></span>

| <span data-ttu-id="62c13-188">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-188">Transform</span></span> | <span data-ttu-id="62c13-189">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-189">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.FeatureSelectionCatalog.SelectFeaturesBasedOnCount%2A> | <span data-ttu-id="62c13-190">选择非默认值大于阈值的功能</span><span class="sxs-lookup"><span data-stu-id="62c13-190">Select features whose non-default values are greater than a threshold</span></span> |
| <xref:Microsoft.ML.FeatureSelectionCatalog.SelectFeaturesBasedOnMutualInformation%2A> | <span data-ttu-id="62c13-191">选择标签列中的数据最依赖的功能</span><span class="sxs-lookup"><span data-stu-id="62c13-191">Select the features on which the data in the label column is most dependent</span></span> |

## <a name="feature-transformations"></a><span data-ttu-id="62c13-192">功能转换</span><span class="sxs-lookup"><span data-stu-id="62c13-192">Feature transformations</span></span>

| <span data-ttu-id="62c13-193">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-193">Transform</span></span> | <span data-ttu-id="62c13-194">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-194">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.KernelExpansionCatalog.ApproximatedKernelMap%2A> | <span data-ttu-id="62c13-195">将每个输入向量映射到较低维度的特征空间，在该特征空间中，内积近似于内核函数，这样就可以将特征用作线性算法的输入</span><span class="sxs-lookup"><span data-stu-id="62c13-195">Map each input vector onto a lower dimensional feature space, where inner products approximate a kernel function, so that the features can be used as inputs to the linear algorithms</span></span> |
| <xref:Microsoft.ML.PcaCatalog.ProjectToPrincipalComponents%2A> | <span data-ttu-id="62c13-196">通过应用主成分分析算法来降低输入特征向量的维度</span><span class="sxs-lookup"><span data-stu-id="62c13-196">Reduce the dimensions of the input feature vector by applying the Principal Component Analysis algorithm</span></span> |

## <a name="explainability-transformations"></a><span data-ttu-id="62c13-197">解释能力转换</span><span class="sxs-lookup"><span data-stu-id="62c13-197">Explainability transformations</span></span>

| <span data-ttu-id="62c13-198">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-198">Transform</span></span> | <span data-ttu-id="62c13-199">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-199">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.ExplainabilityCatalog.CalculateFeatureContribution%2A> | <span data-ttu-id="62c13-200">计算特征向量的每个元素的贡献分数</span><span class="sxs-lookup"><span data-stu-id="62c13-200">Calculate contribution scores for each element of a feature vector</span></span> |

## <a name="calibration-transformations"></a><span data-ttu-id="62c13-201">校准转换</span><span class="sxs-lookup"><span data-stu-id="62c13-201">Calibration transformations</span></span>

| <span data-ttu-id="62c13-202">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-202">Transform</span></span> | <span data-ttu-id="62c13-203">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-203">Definition</span></span> |
| --- | --- |
|<xref:Microsoft.ML.BinaryClassificationCatalog.CalibratorsCatalog.Platt%28System.String%2CSystem.String%2CSystem.String%29> | <span data-ttu-id="62c13-204">使用带有使用训练数据的参数估计的逻辑回归将二元分类器原始分数转换为类概率</span><span class="sxs-lookup"><span data-stu-id="62c13-204">Transforms a binary classifier raw score into a class probability using logistic regression with parameters estimated using the training data</span></span> |
| <xref:Microsoft.ML.BinaryClassificationCatalog.CalibratorsCatalog.Platt%28System.Double%2CSystem.Double%2CSystem.String%29> | <span data-ttu-id="62c13-205">使用带有固定参数的逻辑回归将二元分类器原始分数转换为类概率</span><span class="sxs-lookup"><span data-stu-id="62c13-205">Transforms a binary classifier raw score into a class probability using logistic regression with fixed parameters</span></span> |
| <xref:Microsoft.ML.BinaryClassificationCatalog.CalibratorsCatalog.Naive%2A> | <span data-ttu-id="62c13-206">通过将分数分配到箱并根据箱之间的分布计算概率将二元分类器原始分数转换为类概率</span><span class="sxs-lookup"><span data-stu-id="62c13-206">Transforms a binary classifier raw score into a class probability by assigning scores to bins, and calculating the probability based on the distribution among the bins</span></span> |
| <xref:Microsoft.ML.BinaryClassificationCatalog.CalibratorsCatalog.Isotonic%2A> | <span data-ttu-id="62c13-207">通过将分数分配到箱将二元分类器原始分数转换为类概率（使用训练数据估计边界位置和箱的大小）</span><span class="sxs-lookup"><span data-stu-id="62c13-207">Transforms a binary classifier raw score into a class probability by assigning scores to bins, where the position of boundaries and the size of bins are estimated using the training data</span></span>  |

## <a name="deep-learning-transformations"></a><span data-ttu-id="62c13-208">深度学习转换</span><span class="sxs-lookup"><span data-stu-id="62c13-208">Deep learning transformations</span></span>

| <span data-ttu-id="62c13-209">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-209">Transform</span></span> | <span data-ttu-id="62c13-210">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-210">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.OnnxCatalog.ApplyOnnxModel%2A> | <span data-ttu-id="62c13-211">使用导入的 ONNX 模型转换输入数据</span><span class="sxs-lookup"><span data-stu-id="62c13-211">Transform the input data with an imported ONNX model</span></span> |
| <xref:Microsoft.ML.TensorflowCatalog.LoadTensorFlowModel%2A> | <span data-ttu-id="62c13-212">使用导入的 TensorFlow 模型转换输入数据</span><span class="sxs-lookup"><span data-stu-id="62c13-212">Transform the input data with an imported TensorFlow model</span></span> |

## <a name="custom-transformations"></a><span data-ttu-id="62c13-213">自定义转换</span><span class="sxs-lookup"><span data-stu-id="62c13-213">Custom transformations</span></span>

| <span data-ttu-id="62c13-214">转换</span><span class="sxs-lookup"><span data-stu-id="62c13-214">Transform</span></span> | <span data-ttu-id="62c13-215">定义</span><span class="sxs-lookup"><span data-stu-id="62c13-215">Definition</span></span> |
| --- | --- |
| <xref:Microsoft.ML.CustomMappingCatalog.CustomMapping%2A> | <span data-ttu-id="62c13-216">使用用户定义映射将现有列转换为新列</span><span class="sxs-lookup"><span data-stu-id="62c13-216">Transform existing columns onto new ones with a user-defined mapping</span></span> |
