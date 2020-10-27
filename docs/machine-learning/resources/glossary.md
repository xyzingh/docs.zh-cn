---
title: 机器学习库
description: 一个重要的机器学习术语表，可在 ML.NET 中生成自定义模型时使用。
ms.topic: reference
ms.date: 07/31/2019
ms.openlocfilehash: 32ccb6df1cb08db45ebd25a0d1c0ea4396a6c50b
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223745"
---
# <a name="machine-learning-glossary-of-important-terms"></a><span data-ttu-id="0c79c-103">机器学习重要术语词汇表</span><span class="sxs-lookup"><span data-stu-id="0c79c-103">Machine learning glossary of important terms</span></span>

<span data-ttu-id="0c79c-104">以下列表是重要的机器学习术语编译，可在 ML.NET 中生成自定义模型时使用。</span><span class="sxs-lookup"><span data-stu-id="0c79c-104">The following list is a compilation of important machine learning terms that are useful as you build your custom models in ML.NET.</span></span>

## <a name="accuracy"></a><span data-ttu-id="0c79c-105">精确度</span><span class="sxs-lookup"><span data-stu-id="0c79c-105">Accuracy</span></span>

<span data-ttu-id="0c79c-106">在[分类](#classification)中，准确性是正确分类的项数目除以测试集内的项总数。</span><span class="sxs-lookup"><span data-stu-id="0c79c-106">In [classification](#classification), accuracy is the number of correctly classified items divided by the total number of items in the test set.</span></span> <span data-ttu-id="0c79c-107">范围从 0（最不准确）到 1（最准确）。</span><span class="sxs-lookup"><span data-stu-id="0c79c-107">Ranges from 0 (least accurate) to 1 (most accurate).</span></span> <span data-ttu-id="0c79c-108">准确性是模型性能的评估指标之一。</span><span class="sxs-lookup"><span data-stu-id="0c79c-108">Accuracy is one of evaluation metrics of the model performance.</span></span> <span data-ttu-id="0c79c-109">将其与[精度](#precision)、[撤回](#recall)和 [F 分数](#f-score)结合考虑。</span><span class="sxs-lookup"><span data-stu-id="0c79c-109">Consider it in conjunction with [precision](#precision), [recall](#recall), and [F-score](#f-score).</span></span>

## <a name="area-under-the-curve-auc"></a><span data-ttu-id="0c79c-110">曲线下面积 (AUC)</span><span class="sxs-lookup"><span data-stu-id="0c79c-110">Area under the curve (AUC)</span></span>

<span data-ttu-id="0c79c-111">[二元分类](#binary-classification)中的一项评估指标，即曲线下面积值，它绘制真阳性率（y 轴）与误报率（x 轴）进行对照。</span><span class="sxs-lookup"><span data-stu-id="0c79c-111">In [binary classification](#binary-classification), an evaluation metric that is the value of the area under the curve that plots the true positives rate (on the y-axis) against the false positives rate (on the x-axis).</span></span> <span data-ttu-id="0c79c-112">范围从 0.5（最差）到 1（最佳）。</span><span class="sxs-lookup"><span data-stu-id="0c79c-112">Ranges from 0.5 (worst) to 1 (best).</span></span> <span data-ttu-id="0c79c-113">也称为 ROC 曲线下面积，即，接受者操作特征曲线。</span><span class="sxs-lookup"><span data-stu-id="0c79c-113">Also known as the area under the ROC curve, i.e., receiver operating characteristic curve.</span></span> <span data-ttu-id="0c79c-114">有关详细信息，请参阅 Wikipedia 上的[接受者操作特征](https://en.wikipedia.org/wiki/Receiver_operating_characteristic)一文。</span><span class="sxs-lookup"><span data-stu-id="0c79c-114">For more information, see the [Receiver operating characteristic](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) article on Wikipedia.</span></span>

## <a name="binary-classification"></a><span data-ttu-id="0c79c-115">二元分类</span><span class="sxs-lookup"><span data-stu-id="0c79c-115">Binary classification</span></span>

<span data-ttu-id="0c79c-116">一个[分类](#classification)事例，其中[标签](#label)仅为两个类中的一个。</span><span class="sxs-lookup"><span data-stu-id="0c79c-116">A [classification](#classification) case where the [label](#label) is only one out of two classes.</span></span> <span data-ttu-id="0c79c-117">有关详细信息，请参阅[机器学习任务](tasks.md)主题的[二元分类](tasks.md#binary-classification)部分。</span><span class="sxs-lookup"><span data-stu-id="0c79c-117">For more information, see the [Binary classification](tasks.md#binary-classification) section of the [Machine learning tasks](tasks.md) topic.</span></span>

## <a name="calibration"></a><span data-ttu-id="0c79c-118">校准</span><span class="sxs-lookup"><span data-stu-id="0c79c-118">Calibration</span></span>

<span data-ttu-id="0c79c-119">校准是将原始分数映射到类成员身份的过程，用于二元和多类分类。</span><span class="sxs-lookup"><span data-stu-id="0c79c-119">Calibration is the process of mapping a raw score onto a class membership, for binary and multiclass classification.</span></span> <span data-ttu-id="0c79c-120">一些 ML.NET 训练程序的后缀为 `NonCalibrated`。</span><span class="sxs-lookup"><span data-stu-id="0c79c-120">Some ML.NET trainers have a `NonCalibrated` suffix.</span></span> <span data-ttu-id="0c79c-121">这些算法会生成一个原始分数，该分数之后必须映射到类概率。</span><span class="sxs-lookup"><span data-stu-id="0c79c-121">These algorithms produce a raw score that then must be mapped to a class probability.</span></span>

## <a name="catalog"></a><span data-ttu-id="0c79c-122">目录</span><span class="sxs-lookup"><span data-stu-id="0c79c-122">Catalog</span></span>

<span data-ttu-id="0c79c-123">在 ML.NET 中，目录是扩展函数的集合，按常见用途进行分组。</span><span class="sxs-lookup"><span data-stu-id="0c79c-123">In ML.NET, a catalog is a collection of extension functions, grouped by a common purpose.</span></span>

<span data-ttu-id="0c79c-124">例如，每个机器学习任务（二元分类、回归、排名等）都有一个可用机器学习算法（训练程序）目录。</span><span class="sxs-lookup"><span data-stu-id="0c79c-124">For example, each machine learning task (binary classification, regression, ranking etc) has a catalog of available machine learning algorithms (trainers).</span></span> <span data-ttu-id="0c79c-125">二元分类训练程序的目录是：<xref:Microsoft.ML.BinaryClassificationCatalog.BinaryClassificationTrainers>。</span><span class="sxs-lookup"><span data-stu-id="0c79c-125">The catalog for the binary classification trainers is: <xref:Microsoft.ML.BinaryClassificationCatalog.BinaryClassificationTrainers>.</span></span>

## <a name="classification"></a><span data-ttu-id="0c79c-126">分类</span><span class="sxs-lookup"><span data-stu-id="0c79c-126">Classification</span></span>

<span data-ttu-id="0c79c-127">当使用这些数据来预测某一类别，[监管式机器学习](#supervised-machine-learning)任务被称为“分类”。</span><span class="sxs-lookup"><span data-stu-id="0c79c-127">When the data is used to predict a category, [supervised machine learning](#supervised-machine-learning) task is called classification.</span></span> <span data-ttu-id="0c79c-128">[二元分类](#binary-classification)指的是仅预测两个类别（例如，将图像划分为“猫”或“狗”图片）。</span><span class="sxs-lookup"><span data-stu-id="0c79c-128">[Binary classification](#binary-classification) refers to predicting only two categories (for example, classifying an image as a picture of either a 'cat' or a 'dog').</span></span> <span data-ttu-id="0c79c-129">[多类分类](#multiclass-classification)指的是预测多个类别（例如，当将图像划分为特定品种狗的图片）。</span><span class="sxs-lookup"><span data-stu-id="0c79c-129">[Multiclass classification](#multiclass-classification) refers to predicting multiple categories (for example, when classifying an image as a picture of a specific breed of dog).</span></span>

## <a name="coefficient-of-determination"></a><span data-ttu-id="0c79c-130">决定系数</span><span class="sxs-lookup"><span data-stu-id="0c79c-130">Coefficient of determination</span></span>

<span data-ttu-id="0c79c-131">[回归](#regression)中的一项评估指标，表明数据与模型的匹配程度。</span><span class="sxs-lookup"><span data-stu-id="0c79c-131">In [regression](#regression), an evaluation metric that indicates how well data fits a model.</span></span> <span data-ttu-id="0c79c-132">范围从 0 到 1。</span><span class="sxs-lookup"><span data-stu-id="0c79c-132">Ranges from 0 to 1.</span></span> <span data-ttu-id="0c79c-133">值 0 表示数据是随机的，否则就无法与模型相匹配。</span><span class="sxs-lookup"><span data-stu-id="0c79c-133">A value of 0 means that the data is random or otherwise cannot be fit to the model.</span></span> <span data-ttu-id="0c79c-134">值 1 表示模型与数据完全匹配。</span><span class="sxs-lookup"><span data-stu-id="0c79c-134">A value of 1 means that the model exactly matches the data.</span></span> <span data-ttu-id="0c79c-135">这通常称为 <sup>2</sup>、R<sup>2</sup> 或 r 平方值。</span><span class="sxs-lookup"><span data-stu-id="0c79c-135">This is often referred to as r<sup>2</sup>, R<sup>2</sup>, or r-squared.</span></span>

## <a name="data"></a><span data-ttu-id="0c79c-136">数据</span><span class="sxs-lookup"><span data-stu-id="0c79c-136">Data</span></span>

<span data-ttu-id="0c79c-137">数据是所有机器学习应用程序的核心。</span><span class="sxs-lookup"><span data-stu-id="0c79c-137">Data is central to any machine learning application.</span></span> <span data-ttu-id="0c79c-138">在 ML.NET 中，数据由 <xref:Microsoft.ML.IDataView> 对象表示。</span><span class="sxs-lookup"><span data-stu-id="0c79c-138">In ML.NET data is represented by <xref:Microsoft.ML.IDataView> objects.</span></span> <span data-ttu-id="0c79c-139">数据视图对象：</span><span class="sxs-lookup"><span data-stu-id="0c79c-139">Data view objects:</span></span>

- <span data-ttu-id="0c79c-140">由列和行组成</span><span class="sxs-lookup"><span data-stu-id="0c79c-140">are made up of columns and rows</span></span>
- <span data-ttu-id="0c79c-141">延迟计算，即它们仅在操作调用数据时加载数据</span><span class="sxs-lookup"><span data-stu-id="0c79c-141">are lazily evaluated, that is they only load data when an operation calls for it</span></span>
- <span data-ttu-id="0c79c-142">包含定义了每个列的类型、格式和长度的架构</span><span class="sxs-lookup"><span data-stu-id="0c79c-142">contain a schema that defines the type, format and length of each column</span></span>

## <a name="estimator"></a><span data-ttu-id="0c79c-143">估算器</span><span class="sxs-lookup"><span data-stu-id="0c79c-143">Estimator</span></span>

<span data-ttu-id="0c79c-144">ML.NET 中实现 <xref:Microsoft.ML.IEstimator%601> 接口的类。</span><span class="sxs-lookup"><span data-stu-id="0c79c-144">A class in ML.NET that implements the <xref:Microsoft.ML.IEstimator%601> interface.</span></span>

<span data-ttu-id="0c79c-145">估算器是一种转换（数据准备转换和机器学习模型训练转换）规范。</span><span class="sxs-lookup"><span data-stu-id="0c79c-145">An estimator is a specification of a transformation (both data preparation transformation and machine learning model training transformation).</span></span> <span data-ttu-id="0c79c-146">估算器可以链接在一起形成转换管道。</span><span class="sxs-lookup"><span data-stu-id="0c79c-146">Estimators can be chained together into a pipeline of transformations.</span></span> <span data-ttu-id="0c79c-147">调用 <xref:Microsoft.ML.IEstimator%601.Fit%2A> 时，会学习估算器或估算器管道的参数。</span><span class="sxs-lookup"><span data-stu-id="0c79c-147">The parameters of an estimator or pipeline of estimators are learned when <xref:Microsoft.ML.IEstimator%601.Fit%2A> is called.</span></span> <span data-ttu-id="0c79c-148"><xref:Microsoft.ML.IEstimator%601.Fit%2A> 的结果为[转换器](#transformer)。</span><span class="sxs-lookup"><span data-stu-id="0c79c-148">The result of <xref:Microsoft.ML.IEstimator%601.Fit%2A> is a [Transformer](#transformer).</span></span>

## <a name="extension-method"></a><span data-ttu-id="0c79c-149">扩展方法</span><span class="sxs-lookup"><span data-stu-id="0c79c-149">Extension method</span></span>

<span data-ttu-id="0c79c-150">一种 .NET 方法，它是类的一部分，但在类外部定义。</span><span class="sxs-lookup"><span data-stu-id="0c79c-150">A .NET method that is part of a class but is defined outside of the class.</span></span> <span data-ttu-id="0c79c-151">扩展方法的第一个参数是对扩展方法所属的类的静态 `this` 引用。</span><span class="sxs-lookup"><span data-stu-id="0c79c-151">The first parameter of an extension method is a static `this` reference to the class to which the extension method belongs.</span></span>

<span data-ttu-id="0c79c-152">扩展方法在 ML.NET 中广泛用于构造[估算器](#estimator)实例。</span><span class="sxs-lookup"><span data-stu-id="0c79c-152">Extension methods are used extensively in ML.NET to construct instances of [estimators](#estimator).</span></span>

## <a name="feature"></a><span data-ttu-id="0c79c-153">功能</span><span class="sxs-lookup"><span data-stu-id="0c79c-153">Feature</span></span>

<span data-ttu-id="0c79c-154">正在对其进行度量的现象的一个可度量属性，通常是一个数（双精度）值。</span><span class="sxs-lookup"><span data-stu-id="0c79c-154">A measurable property of the phenomenon being measured, typically a numeric (double) value.</span></span> <span data-ttu-id="0c79c-155">多个特征被称为“特征向量”  且通常存储为 `double[]`。</span><span class="sxs-lookup"><span data-stu-id="0c79c-155">Multiple features are referred to as a **Feature vector** and typically stored as `double[]`.</span></span> <span data-ttu-id="0c79c-156">这些特征定义所度量现象的重要特性。</span><span class="sxs-lookup"><span data-stu-id="0c79c-156">Features define the important characteristics of the phenomenon being measured.</span></span> <span data-ttu-id="0c79c-157">有关详细信息，请参阅 Wikipedia 上的[特征](https://en.wikipedia.org/wiki/Feature_(machine_learning))一文。</span><span class="sxs-lookup"><span data-stu-id="0c79c-157">For more information, see the [Feature](https://en.wikipedia.org/wiki/Feature_(machine_learning)) article on Wikipedia.</span></span>

## <a name="feature-engineering"></a><span data-ttu-id="0c79c-158">特性工程</span><span class="sxs-lookup"><span data-stu-id="0c79c-158">Feature engineering</span></span>

<span data-ttu-id="0c79c-159">特征工程是涉及定义一组[特征](#feature)和开发软件以从可用现象数据中生成特征向量（即特征提取）的过程。</span><span class="sxs-lookup"><span data-stu-id="0c79c-159">Feature engineering is the process that involves defining a set of [features](#feature) and developing software that produces feature vectors from available phenomenon data, i.e., feature extraction.</span></span> <span data-ttu-id="0c79c-160">有关详细信息，请参阅 Wikipedia 上的[特征工程](https://en.wikipedia.org/wiki/Feature_engineering)一文。</span><span class="sxs-lookup"><span data-stu-id="0c79c-160">For more information, see the [Feature engineering](https://en.wikipedia.org/wiki/Feature_engineering) article on Wikipedia.</span></span>

## <a name="f-score"></a><span data-ttu-id="0c79c-161">F 分数</span><span class="sxs-lookup"><span data-stu-id="0c79c-161">F-score</span></span>

<span data-ttu-id="0c79c-162">[分类](#classification)中的一项评估指标，它平衡[精度](#precision)和[撤回](#recall)。</span><span class="sxs-lookup"><span data-stu-id="0c79c-162">In [classification](#classification), an evaluation metric that balances [precision](#precision) and [recall](#recall).</span></span>

## <a name="hyperparameter"></a><span data-ttu-id="0c79c-163">超参数</span><span class="sxs-lookup"><span data-stu-id="0c79c-163">Hyperparameter</span></span>

<span data-ttu-id="0c79c-164">机器学习算法的参数。</span><span class="sxs-lookup"><span data-stu-id="0c79c-164">A parameter of a machine learning algorithm.</span></span> <span data-ttu-id="0c79c-165">示例包括在决策林中学习的树的数量，或者梯度下降算法中的步长。</span><span class="sxs-lookup"><span data-stu-id="0c79c-165">Examples include the number of trees to learn in a decision forest or the step size in a gradient descent algorithm.</span></span> <span data-ttu-id="0c79c-166">在对模型进行定型之前，先设置超参数  的值，并控制查找预测函数参数的过程，例如，决策树中的比较点或线性回归模型中的权重。</span><span class="sxs-lookup"><span data-stu-id="0c79c-166">Values of *Hyperparameters* are set before training the model and govern the process of finding the parameters of the prediction function, for example, the comparison points in a decision tree or the weights in a linear regression model.</span></span> <span data-ttu-id="0c79c-167">有关详细信息，请参阅 Wikipedia 上的[超参数](https://en.wikipedia.org/wiki/Hyperparameter_(machine_learning))一文。</span><span class="sxs-lookup"><span data-stu-id="0c79c-167">For more information, see the [Hyperparameter](https://en.wikipedia.org/wiki/Hyperparameter_(machine_learning)) article on Wikipedia.</span></span>

## <a name="label"></a><span data-ttu-id="0c79c-168">Label</span><span class="sxs-lookup"><span data-stu-id="0c79c-168">Label</span></span>

<span data-ttu-id="0c79c-169">使用机器学习模型进行预测的元素。</span><span class="sxs-lookup"><span data-stu-id="0c79c-169">The element to be predicted with the machine learning model.</span></span> <span data-ttu-id="0c79c-170">例如，狗的品种或将来的股票价格。</span><span class="sxs-lookup"><span data-stu-id="0c79c-170">For example, the breed of dog or a future stock price.</span></span>

## <a name="log-loss"></a><span data-ttu-id="0c79c-171">对数损失</span><span class="sxs-lookup"><span data-stu-id="0c79c-171">Log loss</span></span>

<span data-ttu-id="0c79c-172">在[分类](#classification)中，描述分类器准确性的评估指标。</span><span class="sxs-lookup"><span data-stu-id="0c79c-172">In [classification](#classification), an evaluation metric that characterizes the accuracy of a classifier.</span></span> <span data-ttu-id="0c79c-173">对数损失越小，分类器越准确。</span><span class="sxs-lookup"><span data-stu-id="0c79c-173">The smaller log loss is, the more accurate a classifier is.</span></span>

## <a name="loss-function"></a><span data-ttu-id="0c79c-174">损失函数</span><span class="sxs-lookup"><span data-stu-id="0c79c-174">Loss function</span></span>

<span data-ttu-id="0c79c-175">损失函数是指训练标签值与模型所做预测之间的差异。</span><span class="sxs-lookup"><span data-stu-id="0c79c-175">A loss function is the difference between the training label values and the prediction made by the model.</span></span> <span data-ttu-id="0c79c-176">通过最小化损失函数来估算模型参数。</span><span class="sxs-lookup"><span data-stu-id="0c79c-176">The parameters of the model are estimated by minimizing the loss function.</span></span>

<span data-ttu-id="0c79c-177">可以为不同的训练程序配置不同的损失函数。</span><span class="sxs-lookup"><span data-stu-id="0c79c-177">Different trainers can be configured with different loss functions.</span></span>

## <a name="mean-absolute-error-mae"></a><span data-ttu-id="0c79c-178">平均绝对误差 (MAE)</span><span class="sxs-lookup"><span data-stu-id="0c79c-178">Mean absolute error (MAE)</span></span>

<span data-ttu-id="0c79c-179">[回归](#regression)中的一项评估指标，即所有模型误差的平均值，其中模型误差是预测[标签](#label)值和正确标签值之间的差距。</span><span class="sxs-lookup"><span data-stu-id="0c79c-179">In [regression](#regression), an evaluation metric that is the average of all the model errors, where model error is the distance between the predicted [label](#label) value and the correct label value.</span></span>

## <a name="model"></a><span data-ttu-id="0c79c-180">型号</span><span class="sxs-lookup"><span data-stu-id="0c79c-180">Model</span></span>

<span data-ttu-id="0c79c-181">就传统意义而言，它是预测函数的参数。</span><span class="sxs-lookup"><span data-stu-id="0c79c-181">Traditionally, the parameters for the prediction function.</span></span> <span data-ttu-id="0c79c-182">例如，线性回归模型中的权重或决策树中的拆分点。</span><span class="sxs-lookup"><span data-stu-id="0c79c-182">For example, the weights in a linear regression model or the split points in a decision tree.</span></span> <span data-ttu-id="0c79c-183">在 ML.NET 中，一个模型包含预测域对象[标签](#label)所需的所有信息（例如，图像或文本）。</span><span class="sxs-lookup"><span data-stu-id="0c79c-183">In ML.NET, a model contains all the information necessary to predict the [label](#label) of a domain object (for example, image or text).</span></span> <span data-ttu-id="0c79c-184">这意味着 ML.NET 模型包括所需的特征化步骤以及预测函数参数。</span><span class="sxs-lookup"><span data-stu-id="0c79c-184">This means that ML.NET models include the featurization steps necessary as well as the parameters for the prediction function.</span></span>

## <a name="multiclass-classification"></a><span data-ttu-id="0c79c-185">多类分类</span><span class="sxs-lookup"><span data-stu-id="0c79c-185">Multiclass classification</span></span>

<span data-ttu-id="0c79c-186">一个[分类](#classification)事例，其中[标签](#label)是三个或更多类中的一个。</span><span class="sxs-lookup"><span data-stu-id="0c79c-186">A [classification](#classification) case where the [label](#label) is one out of three or more classes.</span></span> <span data-ttu-id="0c79c-187">有关详细信息，请参阅[机器学习任务](tasks.md)主题的[多类分类](tasks.md#multiclass-classification)部分。</span><span class="sxs-lookup"><span data-stu-id="0c79c-187">For more information, see the [Multiclass classification](tasks.md#multiclass-classification) section of the [Machine learning tasks](tasks.md) topic.</span></span>

## <a name="n-gram"></a><span data-ttu-id="0c79c-188">N 元语法</span><span class="sxs-lookup"><span data-stu-id="0c79c-188">N-gram</span></span>

<span data-ttu-id="0c79c-189">文本数据的特征提取方案：N 个单词的任何序列都将转变为[特征](#feature)值。</span><span class="sxs-lookup"><span data-stu-id="0c79c-189">A feature extraction scheme for text data: any sequence of N words turns into a [feature](#feature) value.</span></span>

## <a name="normalization"></a><span data-ttu-id="0c79c-190">标准化</span><span class="sxs-lookup"><span data-stu-id="0c79c-190">Normalization</span></span>

<span data-ttu-id="0c79c-191">标准化是将浮点数据缩放到 0 到 1 之间的值的过程。</span><span class="sxs-lookup"><span data-stu-id="0c79c-191">Normalization is the process of scaling floating point data to values between 0 and 1.</span></span> <span data-ttu-id="0c79c-192">ML.NET 中使用的许多训练算法都需要对输入特征数据进行标准化。</span><span class="sxs-lookup"><span data-stu-id="0c79c-192">Many of the training algorithms used in ML.NET require input feature data to be normalized.</span></span> <span data-ttu-id="0c79c-193">ML.NET 提供了一系列[用于标准化的转换](transforms.md#normalization-and-scaling)</span><span class="sxs-lookup"><span data-stu-id="0c79c-193">ML.NET provides a series of [transforms for normalization](transforms.md#normalization-and-scaling)</span></span>

## <a name="numerical-feature-vector"></a><span data-ttu-id="0c79c-194">数字特征向量</span><span class="sxs-lookup"><span data-stu-id="0c79c-194">Numerical feature vector</span></span>

<span data-ttu-id="0c79c-195">只包含数值的[特征](#feature)向量。</span><span class="sxs-lookup"><span data-stu-id="0c79c-195">A [feature](#feature) vector consisting only of numerical values.</span></span> <span data-ttu-id="0c79c-196">这与 `double[]` 非常类似。</span><span class="sxs-lookup"><span data-stu-id="0c79c-196">This is similar to `double[]`.</span></span>

## <a name="pipeline"></a><span data-ttu-id="0c79c-197">管道</span><span class="sxs-lookup"><span data-stu-id="0c79c-197">Pipeline</span></span>

<span data-ttu-id="0c79c-198">要将模型与数据集相匹配所需的所有操作。</span><span class="sxs-lookup"><span data-stu-id="0c79c-198">All of the operations needed to fit a model to a data set.</span></span> <span data-ttu-id="0c79c-199">管道由数据导入、转换、特征化和学习步骤组成。</span><span class="sxs-lookup"><span data-stu-id="0c79c-199">A pipeline consists of data import, transformation, featurization, and learning steps.</span></span> <span data-ttu-id="0c79c-200">对管道进行定型后，它会转变为模型。</span><span class="sxs-lookup"><span data-stu-id="0c79c-200">Once a pipeline is trained, it turns into a model.</span></span>

## <a name="precision"></a><span data-ttu-id="0c79c-201">Precision</span><span class="sxs-lookup"><span data-stu-id="0c79c-201">Precision</span></span>

<span data-ttu-id="0c79c-202">在[分类](#classification)中，类的精度是正确预测为属于该类的项目的数量，除以预测为属于该类的项目的总数。</span><span class="sxs-lookup"><span data-stu-id="0c79c-202">In [classification](#classification), the precision for a class is the number of items correctly predicted as belonging to that class divided by the total number of items predicted as belonging to the class.</span></span>

## <a name="recall"></a><span data-ttu-id="0c79c-203">Recall</span><span class="sxs-lookup"><span data-stu-id="0c79c-203">Recall</span></span>

<span data-ttu-id="0c79c-204">在[分类](#classification)中，类的撤回是正确预测为属于该类的项目的数量，除以实际属于该类的项目的总数。</span><span class="sxs-lookup"><span data-stu-id="0c79c-204">In [classification](#classification), the recall for a class is the number of items correctly predicted as belonging to that class divided by the total number of items that actually belong to the class.</span></span>

## <a name="regularization"></a><span data-ttu-id="0c79c-205">正则化</span><span class="sxs-lookup"><span data-stu-id="0c79c-205">Regularization</span></span>

 <span data-ttu-id="0c79c-206">正则化会对过于复杂的线性模型进行惩罚。</span><span class="sxs-lookup"><span data-stu-id="0c79c-206">Regularization penalizes a linear model for being too complicated.</span></span> <span data-ttu-id="0c79c-207">正则化有两种类型：</span><span class="sxs-lookup"><span data-stu-id="0c79c-207">There are two types of regularization:</span></span>

- <span data-ttu-id="0c79c-208">$L_1$ 正则化将无意义特征的权重归零。</span><span class="sxs-lookup"><span data-stu-id="0c79c-208">$L_1$ regularization zeros weights for insignificant features.</span></span> <span data-ttu-id="0c79c-209">进行这种正则化之后，所保存模型的大小可能会变小。</span><span class="sxs-lookup"><span data-stu-id="0c79c-209">The size of the saved model may become smaller after this type of regularization.</span></span>
- <span data-ttu-id="0c79c-210">$L_2$ 正则化将无意义特征的权重范围最小化。</span><span class="sxs-lookup"><span data-stu-id="0c79c-210">$L_2$ regularization minimizes weight range for insignificant features.</span></span> <span data-ttu-id="0c79c-211">这是一种更通用的过程，并且对离群值不太敏感。</span><span class="sxs-lookup"><span data-stu-id="0c79c-211">This is a more general process and is less sensitive to outliers.</span></span>

## <a name="regression"></a><span data-ttu-id="0c79c-212">回归</span><span class="sxs-lookup"><span data-stu-id="0c79c-212">Regression</span></span>

<span data-ttu-id="0c79c-213">[监管式机器学习](#supervised-machine-learning)任务，其中输出是一个实际值，例如，双精度值。</span><span class="sxs-lookup"><span data-stu-id="0c79c-213">A [supervised machine learning](#supervised-machine-learning) task where the output is a real value, for example, double.</span></span> <span data-ttu-id="0c79c-214">示例包括预测股票价格。</span><span class="sxs-lookup"><span data-stu-id="0c79c-214">Examples include predicting stock prices.</span></span> <span data-ttu-id="0c79c-215">有关详细信息，请参阅[机器学习任务](tasks.md)主题的[回归](tasks.md#regression)部分。</span><span class="sxs-lookup"><span data-stu-id="0c79c-215">For more information, see the [Regression](tasks.md#regression) section of the [Machine learning tasks](tasks.md) topic.</span></span>

## <a name="relative-absolute-error"></a><span data-ttu-id="0c79c-216">相对绝对误差</span><span class="sxs-lookup"><span data-stu-id="0c79c-216">Relative absolute error</span></span>

<span data-ttu-id="0c79c-217">[回归](#regression)中的一项评估指标，即所有绝对误差总和除以正确[标签](#label)值和所有正确标签值的平均值之间的差值总和。</span><span class="sxs-lookup"><span data-stu-id="0c79c-217">In [regression](#regression), an evaluation metric that is the sum of all absolute errors divided by the sum of distances between correct [label](#label) values and the average of all correct label values.</span></span>

## <a name="relative-squared-error"></a><span data-ttu-id="0c79c-218">相对平方误差</span><span class="sxs-lookup"><span data-stu-id="0c79c-218">Relative squared error</span></span>

<span data-ttu-id="0c79c-219">[回归](#regression)中的一项评估指标，即所有绝对平方误差总和除以正确[标签](#label)值和所有正确标签值的平均值之间的平方差值总和。</span><span class="sxs-lookup"><span data-stu-id="0c79c-219">In [regression](#regression), an evaluation metric that is the sum of all squared absolute errors divided by the sum of squared distances between correct [label](#label) values and the average of all correct label values.</span></span>

## <a name="root-of-mean-squared-error-rmse"></a><span data-ttu-id="0c79c-220">均方误差根 (RMSE)</span><span class="sxs-lookup"><span data-stu-id="0c79c-220">Root of mean squared error (RMSE)</span></span>

<span data-ttu-id="0c79c-221">[回归](#regression)中的一项评估指标，即误差平方平均值的平方根。</span><span class="sxs-lookup"><span data-stu-id="0c79c-221">In [regression](#regression), an evaluation metric that is the square root of the average of the squares of the errors.</span></span>

## <a name="scoring"></a><span data-ttu-id="0c79c-222">计分</span><span class="sxs-lookup"><span data-stu-id="0c79c-222">Scoring</span></span>

<span data-ttu-id="0c79c-223">评分是将新数据应用于经过训练的机器学习模型并生成预测的过程。</span><span class="sxs-lookup"><span data-stu-id="0c79c-223">Scoring is the process of applying new data to a trained machine learning model, and generating predictions.</span></span> <span data-ttu-id="0c79c-224">评分也称为推断。</span><span class="sxs-lookup"><span data-stu-id="0c79c-224">Scoring is also known as inferencing.</span></span> <span data-ttu-id="0c79c-225">根据模型类型，分数可以是原始值、概率或类别。</span><span class="sxs-lookup"><span data-stu-id="0c79c-225">Depending on the type of model, the score may be a raw value, a probability, or a category.</span></span>

## <a name="supervised-machine-learning"></a><span data-ttu-id="0c79c-226">监管式机器学习</span><span class="sxs-lookup"><span data-stu-id="0c79c-226">Supervised machine learning</span></span>

<span data-ttu-id="0c79c-227">机器学习的一个子类，其中所需的模型预测尚不可见的数据标签。</span><span class="sxs-lookup"><span data-stu-id="0c79c-227">A subclass of machine learning in which a desired model predicts the label for yet-unseen data.</span></span> <span data-ttu-id="0c79c-228">示例包括分类、回归以及结构化预测。</span><span class="sxs-lookup"><span data-stu-id="0c79c-228">Examples include classification, regression, and structured prediction.</span></span> <span data-ttu-id="0c79c-229">有关详细信息，请参阅 Wikipedia 上的[监管式学习](https://en.wikipedia.org/wiki/Supervised_learning)一文。</span><span class="sxs-lookup"><span data-stu-id="0c79c-229">For more information, see the  [Supervised learning](https://en.wikipedia.org/wiki/Supervised_learning) article on Wikipedia.</span></span>

## <a name="training"></a><span data-ttu-id="0c79c-230">培训</span><span class="sxs-lookup"><span data-stu-id="0c79c-230">Training</span></span>

<span data-ttu-id="0c79c-231">识别给定定型数据集[模型](#model)的过程。</span><span class="sxs-lookup"><span data-stu-id="0c79c-231">The process of identifying a [model](#model) for a given training data set.</span></span> <span data-ttu-id="0c79c-232">对于线性模型，这意味着查找权重。</span><span class="sxs-lookup"><span data-stu-id="0c79c-232">For a linear model, this means finding the weights.</span></span> <span data-ttu-id="0c79c-233">有关树信息，这涉及到标识拆分点。</span><span class="sxs-lookup"><span data-stu-id="0c79c-233">For a tree, it involves identifying the split points.</span></span>

## <a name="transformer"></a><span data-ttu-id="0c79c-234">转换器</span><span class="sxs-lookup"><span data-stu-id="0c79c-234">Transformer</span></span>

<span data-ttu-id="0c79c-235">一个实现 <xref:Microsoft.ML.ITransformer> 接口的 ML.NET 类。</span><span class="sxs-lookup"><span data-stu-id="0c79c-235">An ML.NET class that implements the <xref:Microsoft.ML.ITransformer> interface.</span></span>

<span data-ttu-id="0c79c-236">转换器可将一个 <xref:Microsoft.ML.IDataView> 转换为另一个 IDataView。</span><span class="sxs-lookup"><span data-stu-id="0c79c-236">A transformer transforms one <xref:Microsoft.ML.IDataView> into another.</span></span> <span data-ttu-id="0c79c-237">转换器是通过训练[估算器](#estimator)或估算器管道创建的。</span><span class="sxs-lookup"><span data-stu-id="0c79c-237">A transformer is created by training an [estimator](#estimator), or an estimator pipeline.</span></span>

## <a name="unsupervised-machine-learning"></a><span data-ttu-id="0c79c-238">非监管式机器学习</span><span class="sxs-lookup"><span data-stu-id="0c79c-238">Unsupervised machine learning</span></span>

<span data-ttu-id="0c79c-239">机器学习的子类，其中所需的模型查找数据中的隐藏（或潜在）结构。</span><span class="sxs-lookup"><span data-stu-id="0c79c-239">A subclass of machine learning in which a desired model finds hidden (or latent) structure in data.</span></span> <span data-ttu-id="0c79c-240">示例包括聚类分析、主题建模和维数约简。</span><span class="sxs-lookup"><span data-stu-id="0c79c-240">Examples include clustering, topic modeling, and dimensionality reduction.</span></span> <span data-ttu-id="0c79c-241">有关详细信息，请参阅 Wikipedia 上的[非监管式学习](https://en.wikipedia.org/wiki/Unsupervised_learning)一文。</span><span class="sxs-lookup"><span data-stu-id="0c79c-241">For more information, see the [Unsupervised learning](https://en.wikipedia.org/wiki/Unsupervised_learning) article on Wikipedia.</span></span>
