---
title: 什么是模型生成器，它的工作原理是怎样的？
description: 如何使用 ML.NET 模型生成器自动训练机器学习模型
ms.date: 06/01/2020
ms.custom: overview, mlnet-tooling
ms.openlocfilehash: da6348fb5dde83827558b66b6115d681f08948db
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92161135"
---
# <a name="what-is-model-builder-and-how-does-it-work"></a><span data-ttu-id="4fea5-103">什么是模型生成器，它的工作原理是怎样的？</span><span class="sxs-lookup"><span data-stu-id="4fea5-103">What is Model Builder and how does it work?</span></span>

<span data-ttu-id="4fea5-104">ML.NET 模型生成器是一个直观的图形化 Visual Studio 扩展，用于生成、训练和部署自定义机器学习模型。</span><span class="sxs-lookup"><span data-stu-id="4fea5-104">ML.NET Model Builder is an intuitive graphical Visual Studio extension to build, train, and deploy custom machine learning models.</span></span>

<span data-ttu-id="4fea5-105">模型生成器使用自动化的机器学习 (AutoML) 来探索不同的机器学习算法和设置，以帮助找到最合适的方案。</span><span class="sxs-lookup"><span data-stu-id="4fea5-105">Model Builder uses automated machine learning (AutoML) to explore different machine learning algorithms and settings to help you find the one that best suits your scenario.</span></span>

<span data-ttu-id="4fea5-106">使用模型生成器不需要具备机器学习的专业知识。</span><span class="sxs-lookup"><span data-stu-id="4fea5-106">You don't need machine learning expertise to use Model Builder.</span></span> <span data-ttu-id="4fea5-107">只需要一些数据，和确定要解决的问题。</span><span class="sxs-lookup"><span data-stu-id="4fea5-107">All you need is some data, and a problem to solve.</span></span> <span data-ttu-id="4fea5-108">模型生成器会生成将模型添加到 .NET 应用程序的代码。</span><span class="sxs-lookup"><span data-stu-id="4fea5-108">Model Builder generates the code to add the model to your .NET application.</span></span>

![模型生成器 Visual Studio 扩展用户界面动画](media/ml-dotnet-model-builder.gif)

> [!NOTE]
> <span data-ttu-id="4fea5-110">模型生成器当前为预览版。</span><span class="sxs-lookup"><span data-stu-id="4fea5-110">Model Builder is currently in Preview.</span></span>

## <a name="scenario"></a><span data-ttu-id="4fea5-111">方案</span><span class="sxs-lookup"><span data-stu-id="4fea5-111">Scenario</span></span>

<span data-ttu-id="4fea5-112">可以为模型生成器提供许多不同的方案，从而为应用程序生成一个机器学习模型。</span><span class="sxs-lookup"><span data-stu-id="4fea5-112">You can bring many different scenarios to Model Builder, to generate a machine learning model for your application.</span></span>

<span data-ttu-id="4fea5-113">方案就是要使用数据进行预测类型的描述。</span><span class="sxs-lookup"><span data-stu-id="4fea5-113">A scenario is a description of the type of prediction you want to make using your data.</span></span> <span data-ttu-id="4fea5-114">例如：</span><span class="sxs-lookup"><span data-stu-id="4fea5-114">For example:</span></span>

- <span data-ttu-id="4fea5-115">根据历史销售数据预测未来的产品销量</span><span class="sxs-lookup"><span data-stu-id="4fea5-115">predict future product sales volume based on historical sales data</span></span>
- <span data-ttu-id="4fea5-116">根据客户评价将情绪分类为正面或负面</span><span class="sxs-lookup"><span data-stu-id="4fea5-116">classify sentiments as positive or negative based on customer reviews</span></span>
- <span data-ttu-id="4fea5-117">检测某项银行交易是否存在欺诈性</span><span class="sxs-lookup"><span data-stu-id="4fea5-117">detect whether a banking transaction is fraudulent</span></span>
- <span data-ttu-id="4fea5-118">将客户反馈问题传递至公司中合适的团队</span><span class="sxs-lookup"><span data-stu-id="4fea5-118">route customer feedback issues to the correct team in your company</span></span>

### <a name="which-machine-learning-scenario-is-right-for-me"></a><span data-ttu-id="4fea5-119">哪个机器学习方案最适合我？</span><span class="sxs-lookup"><span data-stu-id="4fea5-119">Which machine learning scenario is right for me?</span></span>

<span data-ttu-id="4fea5-120">在模型生成器中，你需要选择一个方案。</span><span class="sxs-lookup"><span data-stu-id="4fea5-120">In Model Builder, you need to select a scenario.</span></span> <span data-ttu-id="4fea5-121">方案类型取决于尝试进行的预测类型。</span><span class="sxs-lookup"><span data-stu-id="4fea5-121">The type of scenario depends on what type of prediction you are trying to make.</span></span>

#### <a name="text-classification"></a><span data-ttu-id="4fea5-122">文本分类</span><span class="sxs-lookup"><span data-stu-id="4fea5-122">Text classification</span></span>

<span data-ttu-id="4fea5-123">分类用于将数据分类为类别。</span><span class="sxs-lookup"><span data-stu-id="4fea5-123">Classification is used to categorize data into categories.</span></span>

![显示二元分类示例（包括欺诈检测、风险环节和应用程序屏蔽）的图示](media/binary-classification-examples.png)

![多类分类示例，包括文档和产品分类、支持票证路由以及客户问题优先级](media/multiclass-classification-examples.png)

#### <a name="value-prediction"></a><span data-ttu-id="4fea5-126">值预测</span><span class="sxs-lookup"><span data-stu-id="4fea5-126">Value prediction</span></span>

<span data-ttu-id="4fea5-127">回归用于预测数字。</span><span class="sxs-lookup"><span data-stu-id="4fea5-127">Regression is used to predict numbers.</span></span>

![显示回归示例（如价格预测、销售预测和预测性维护）的图示](media/regression-examples.png)

#### <a name="image-classification"></a><span data-ttu-id="4fea5-129">图像分类</span><span class="sxs-lookup"><span data-stu-id="4fea5-129">Image classification</span></span>

<span data-ttu-id="4fea5-130">图像分类用于标识不同类别的图像。</span><span class="sxs-lookup"><span data-stu-id="4fea5-130">Image classification is used to identify images of different categories.</span></span> <span data-ttu-id="4fea5-131">例如，不同类型的地形或动物或制造缺陷。</span><span class="sxs-lookup"><span data-stu-id="4fea5-131">For example, different types of terrain or animals or manufacturing defects.</span></span>

<span data-ttu-id="4fea5-132">如果你有一组图像，并且想要将图像分为不同的类别，则可以使用图像分类方案。</span><span class="sxs-lookup"><span data-stu-id="4fea5-132">You can use the image classification scenario if you have a set of images, and you want to classify the images into different categories.</span></span>

#### <a name="object-detection"></a><span data-ttu-id="4fea5-133">对象检测</span><span class="sxs-lookup"><span data-stu-id="4fea5-133">Object detection</span></span>

<span data-ttu-id="4fea5-134">对象检测用于定位图像中的实体并对其进行分类。</span><span class="sxs-lookup"><span data-stu-id="4fea5-134">Object detection is used to locate and categorize entities within images.</span></span>  <span data-ttu-id="4fea5-135">例如，定位和识别图像中的汽车和人。</span><span class="sxs-lookup"><span data-stu-id="4fea5-135">For example, locating and identifying cars and people in an image.</span></span>

<span data-ttu-id="4fea5-136">如果图像包含多个不同类型的对象，可使用对象检测。</span><span class="sxs-lookup"><span data-stu-id="4fea5-136">You can use object detection when images contain multiple objects of different types.</span></span>

#### <a name="recommendation"></a><span data-ttu-id="4fea5-137">建议</span><span class="sxs-lookup"><span data-stu-id="4fea5-137">Recommendation</span></span>

<span data-ttu-id="4fea5-138">建议的方案根据特定用户的好恶与其他用户的相似程度，为他们预测建议项列表。</span><span class="sxs-lookup"><span data-stu-id="4fea5-138">The recommendation scenario predicts a list of suggested items for a particular user, based on how similar their likes and dislikes are to other users'.</span></span>

<span data-ttu-id="4fea5-139">当你有一组用户和一组“产品”（如要购买的商品、电影、书籍或电视节目）以及一组用户对这些产品的“评级”时，你可以使用建议的方案。</span><span class="sxs-lookup"><span data-stu-id="4fea5-139">You can use the recommendation scenario when you have a set of users and a set of "products", such as items to purchase, movies, books, or TV shows, along with a set of users' "ratings" of those products.</span></span>

## <a name="environment"></a><span data-ttu-id="4fea5-140">环境</span><span class="sxs-lookup"><span data-stu-id="4fea5-140">Environment</span></span>

<span data-ttu-id="4fea5-141">可以在本地计算机上或在 Azure 上的云中训练机器学习模型，具体取决于相应方案。</span><span class="sxs-lookup"><span data-stu-id="4fea5-141">You can train your machine learning model locally on your machine or in the cloud on Azure, depending on the scenario.</span></span>

<span data-ttu-id="4fea5-142">在本地训练模型时，你将在计算机资源（CPU、内存和磁盘）的约束下工作。</span><span class="sxs-lookup"><span data-stu-id="4fea5-142">When you train locally, you work within the constraints of your computer resources (CPU, memory, and disk).</span></span> <span data-ttu-id="4fea5-143">在云中训练模型时，你可以扩展资源来满足你的方案的需求，尤其是对于大型数据集。</span><span class="sxs-lookup"><span data-stu-id="4fea5-143">When you train in the cloud, you can scale up your resources to meet the demands of your scenario, especially for large datasets.</span></span>

<span data-ttu-id="4fea5-144">除对象检测外，所有方案都支持本地 CPU 训练。</span><span class="sxs-lookup"><span data-stu-id="4fea5-144">Local CPU training is supported for all scenarios except Object Detection.</span></span>

<span data-ttu-id="4fea5-145">图像分类支持本地 GPU 训练。</span><span class="sxs-lookup"><span data-stu-id="4fea5-145">Local GPU training is supported for Image Classification.</span></span>

<span data-ttu-id="4fea5-146">图像分类和对象检测支持 Azure 训练。</span><span class="sxs-lookup"><span data-stu-id="4fea5-146">Azure training is supported for Image Classification and Object Detection.</span></span>

## <a name="data"></a><span data-ttu-id="4fea5-147">数据</span><span class="sxs-lookup"><span data-stu-id="4fea5-147">Data</span></span>

<span data-ttu-id="4fea5-148">选择方案后，模型生成器会要求你提供数据集。</span><span class="sxs-lookup"><span data-stu-id="4fea5-148">Once you have chosen your scenario, Model Builder asks you to provide a dataset.</span></span> <span data-ttu-id="4fea5-149">这些数据用于训练、评估和选择最适合方案的的模型。</span><span class="sxs-lookup"><span data-stu-id="4fea5-149">The data is used to train, evaluate, and choose the best model for your scenario.</span></span>

![显示模型生成器步骤的图示](media/model-builder-steps.png)

<span data-ttu-id="4fea5-151">模型生成器支持 .tsv、.csv、.txt 格式以及 SQL 数据库格式的数据集。</span><span class="sxs-lookup"><span data-stu-id="4fea5-151">Model Builder supports datasets in .tsv, .csv, .txt formats, as well as SQL database format.</span></span> <span data-ttu-id="4fea5-152">如果你有一个 .txt 文件，则应使用 `,`、`;` 或 `/t` 分隔列，并且该文件必须具有标题行。</span><span class="sxs-lookup"><span data-stu-id="4fea5-152">If you have a .txt file, columns should be separated with `,`, `;` or `/t` and the file must have a header row.</span></span>

<span data-ttu-id="4fea5-153">如果数据集由图像组成，则支持的文件类型为 `.jpg` 和 `.png`。</span><span class="sxs-lookup"><span data-stu-id="4fea5-153">If the dataset is made up of images, the supported file types are `.jpg` and `.png`.</span></span>

<span data-ttu-id="4fea5-154">有关详细信息，请参阅[将训练数据加载到模型生成器](how-to-guides/load-data-model-builder.md)。</span><span class="sxs-lookup"><span data-stu-id="4fea5-154">For more information, see [Load training data into Model Builder](how-to-guides/load-data-model-builder.md).</span></span>

### <a name="choose-the-output-to-predict-label"></a><span data-ttu-id="4fea5-155">选择要预测的输出（标签）</span><span class="sxs-lookup"><span data-stu-id="4fea5-155">Choose the output to predict (label)</span></span>

<span data-ttu-id="4fea5-156">数据集是一个表格，其中，行中含训练示例，列中含特性。</span><span class="sxs-lookup"><span data-stu-id="4fea5-156">A dataset is a table of rows of training examples, and columns of attributes.</span></span> <span data-ttu-id="4fea5-157">每一行都具有：</span><span class="sxs-lookup"><span data-stu-id="4fea5-157">Each row has:</span></span>

- <span data-ttu-id="4fea5-158">一个标签，即要预测的特性</span><span class="sxs-lookup"><span data-stu-id="4fea5-158">a **label** (the attribute that you want to predict)</span></span>
- <span data-ttu-id="4fea5-159">特征（为预测标签而用作输入的特性）。</span><span class="sxs-lookup"><span data-stu-id="4fea5-159">**features** (attributes that are used as inputs to predict the label).</span></span>

<span data-ttu-id="4fea5-160">在房价预测方案中，特性可能是：</span><span class="sxs-lookup"><span data-stu-id="4fea5-160">For the house-price prediction scenario, the features could be:</span></span>

- <span data-ttu-id="4fea5-161">房屋的面积</span><span class="sxs-lookup"><span data-stu-id="4fea5-161">the square footage of the house</span></span>
- <span data-ttu-id="4fea5-162">卧室和卫生间的数量</span><span class="sxs-lookup"><span data-stu-id="4fea5-162">the number of bedrooms and bathrooms</span></span>
- <span data-ttu-id="4fea5-163">邮政编码</span><span class="sxs-lookup"><span data-stu-id="4fea5-163">the zip code</span></span>

<span data-ttu-id="4fea5-164">标签是与其所属行（包含面积、卧室和卫生间值以及邮政编码信息）对应的历史房价。</span><span class="sxs-lookup"><span data-stu-id="4fea5-164">The label is the historical house price for that row of square footage, bedroom, and bathroom values and zip code.</span></span>

![表显示房价数据的行和列，其中包含由大小、房间数、邮政编码和价格标签组成的特征](media/model-builder-data.png)

### <a name="example-datasets"></a><span data-ttu-id="4fea5-166">示例数据集</span><span class="sxs-lookup"><span data-stu-id="4fea5-166">Example datasets</span></span>

<span data-ttu-id="4fea5-167">如果还没有自己的数据，请试用以下数据集之一：</span><span class="sxs-lookup"><span data-stu-id="4fea5-167">If you don't have your own data yet, try out one of these datasets:</span></span>

|<span data-ttu-id="4fea5-168">方案</span><span class="sxs-lookup"><span data-stu-id="4fea5-168">Scenario</span></span>|<span data-ttu-id="4fea5-169">示例</span><span class="sxs-lookup"><span data-stu-id="4fea5-169">Example</span></span>|<span data-ttu-id="4fea5-170">数据</span><span class="sxs-lookup"><span data-stu-id="4fea5-170">Data</span></span>|<span data-ttu-id="4fea5-171">Label</span><span class="sxs-lookup"><span data-stu-id="4fea5-171">Label</span></span>|<span data-ttu-id="4fea5-172">特征</span><span class="sxs-lookup"><span data-stu-id="4fea5-172">Features</span></span>|
|-|-|-|-|-|
|<span data-ttu-id="4fea5-173">分类</span><span class="sxs-lookup"><span data-stu-id="4fea5-173">Classification</span></span>|<span data-ttu-id="4fea5-174">预测销售异常</span><span class="sxs-lookup"><span data-stu-id="4fea5-174">Predict sales anomalies</span></span>|[<span data-ttu-id="4fea5-175">产品销售数据</span><span class="sxs-lookup"><span data-stu-id="4fea5-175">product sales data</span></span>](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv)|<span data-ttu-id="4fea5-176">产品销售额</span><span class="sxs-lookup"><span data-stu-id="4fea5-176">Product Sales</span></span>|<span data-ttu-id="4fea5-177">月份</span><span class="sxs-lookup"><span data-stu-id="4fea5-177">Month</span></span>|
||<span data-ttu-id="4fea5-178">预测网站评论的情绪</span><span class="sxs-lookup"><span data-stu-id="4fea5-178">Predict sentiment of website comments</span></span>|[<span data-ttu-id="4fea5-179">网站评论数据</span><span class="sxs-lookup"><span data-stu-id="4fea5-179">website comment data</span></span>](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/wikipedia-detox-250-line-data.tsv)|<span data-ttu-id="4fea5-180">标签（负面情绪为 0，正面情绪为 1）</span><span class="sxs-lookup"><span data-stu-id="4fea5-180">Label (0 when negative sentiment, 1 when positive)</span></span>|<span data-ttu-id="4fea5-181">评论、年份</span><span class="sxs-lookup"><span data-stu-id="4fea5-181">Comment, Year</span></span>|
||<span data-ttu-id="4fea5-182">预测信用卡欺诈交易</span><span class="sxs-lookup"><span data-stu-id="4fea5-182">Predict fraudulent credit card transactions</span></span>|[<span data-ttu-id="4fea5-183">信用卡数据</span><span class="sxs-lookup"><span data-stu-id="4fea5-183">credit card data</span></span>](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/getting-started/BinaryClassification_CreditCardFraudDetection/CCFraudDetection.Trainer/assets/input/creditcardfraud-dataset.zip)|<span data-ttu-id="4fea5-184">类（存在欺诈性为 1，否则为 0）</span><span class="sxs-lookup"><span data-stu-id="4fea5-184">Class (1 when fraudulent, 0 otherwise)</span></span>|<span data-ttu-id="4fea5-185">金额，V1-V28（匿名处理后的特征）</span><span class="sxs-lookup"><span data-stu-id="4fea5-185">Amount, V1-V28 (anonymized features)</span></span>|
||<span data-ttu-id="4fea5-186">预测 GitHub 存储库中的问题类型</span><span class="sxs-lookup"><span data-stu-id="4fea5-186">Predict the type of issue in a GitHub repository</span></span>|[<span data-ttu-id="4fea5-187">GitHub 问题数据</span><span class="sxs-lookup"><span data-stu-id="4fea5-187">GitHub issue data</span></span>](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/end-to-end-apps/MulticlassClassification-GitHubLabeler/GitHubLabeler/Data/corefx-issues-train.tsv)|<span data-ttu-id="4fea5-188">区域</span><span class="sxs-lookup"><span data-stu-id="4fea5-188">Area</span></span>|<span data-ttu-id="4fea5-189">标题、描述</span><span class="sxs-lookup"><span data-stu-id="4fea5-189">Title, Description</span></span>|
|<span data-ttu-id="4fea5-190">值预测</span><span class="sxs-lookup"><span data-stu-id="4fea5-190">Value prediction</span></span>|<span data-ttu-id="4fea5-191">预测出租车费用价格</span><span class="sxs-lookup"><span data-stu-id="4fea5-191">Predict taxi fare price</span></span>|[<span data-ttu-id="4fea5-192">出租车费数据</span><span class="sxs-lookup"><span data-stu-id="4fea5-192">taxi fare data</span></span>](https://github.com/dotnet/machinelearning-samples/blob/master/datasets/taxi-fare-train.csv)|<span data-ttu-id="4fea5-193">车费</span><span class="sxs-lookup"><span data-stu-id="4fea5-193">Fare</span></span>|<span data-ttu-id="4fea5-194">行程时间、距离</span><span class="sxs-lookup"><span data-stu-id="4fea5-194">Trip time, distance</span></span>|
|<span data-ttu-id="4fea5-195">图像分类</span><span class="sxs-lookup"><span data-stu-id="4fea5-195">Image classification</span></span>|<span data-ttu-id="4fea5-196">预测花卉的类别</span><span class="sxs-lookup"><span data-stu-id="4fea5-196">Predict the category of a flower</span></span> |[<span data-ttu-id="4fea5-197">花卉图像</span><span class="sxs-lookup"><span data-stu-id="4fea5-197">flower images</span></span>](http://download.tensorflow.org/example_images/flower_photos.tgz)|<span data-ttu-id="4fea5-198">花卉类型：雏菊、蒲公英、玫瑰、向日葵、郁金香</span><span class="sxs-lookup"><span data-stu-id="4fea5-198">The type of flower: daisy, dandelion, roses, sunflowers, tulips</span></span>|<span data-ttu-id="4fea5-199">图像数据本身</span><span class="sxs-lookup"><span data-stu-id="4fea5-199">The image data itself</span></span>|
|<span data-ttu-id="4fea5-200">建议</span><span class="sxs-lookup"><span data-stu-id="4fea5-200">Recommendation</span></span>|<span data-ttu-id="4fea5-201">预测他人喜欢的电影</span><span class="sxs-lookup"><span data-stu-id="4fea5-201">Predict movies that someone will like</span></span>|[<span data-ttu-id="4fea5-202">电影评分</span><span class="sxs-lookup"><span data-stu-id="4fea5-202">movie ratings</span></span>](http://files.grouplens.org/datasets/movielens/ml-latest-small.zip)|<span data-ttu-id="4fea5-203">用户、电影</span><span class="sxs-lookup"><span data-stu-id="4fea5-203">Users, Movies</span></span>|<span data-ttu-id="4fea5-204">评级</span><span class="sxs-lookup"><span data-stu-id="4fea5-204">Ratings</span></span>|

## <a name="train"></a><span data-ttu-id="4fea5-205">训练</span><span class="sxs-lookup"><span data-stu-id="4fea5-205">Train</span></span>

<span data-ttu-id="4fea5-206">选择方案、环境、数据和标签后，模型生成器会训练该模型。</span><span class="sxs-lookup"><span data-stu-id="4fea5-206">Once you select your scenario, environment, data, and label, Model Builder trains the model.</span></span>

### <a name="what-is-training"></a><span data-ttu-id="4fea5-207">什么是训练？</span><span class="sxs-lookup"><span data-stu-id="4fea5-207">What is training?</span></span>

<span data-ttu-id="4fea5-208">训练是一个自动的过程，模型生成器通过该过程教模型如何回答方案相关的问题。</span><span class="sxs-lookup"><span data-stu-id="4fea5-208">Training is an automatic process by which Model Builder teaches your model how to answer questions for your scenario.</span></span> <span data-ttu-id="4fea5-209">训练后，模型可以对其没有见过的输入数据进行预测。</span><span class="sxs-lookup"><span data-stu-id="4fea5-209">Once trained, your model can make predictions with input data that it has not seen before.</span></span> <span data-ttu-id="4fea5-210">例如，在预测房价时，可以预测新上市的房屋销售价。</span><span class="sxs-lookup"><span data-stu-id="4fea5-210">For example, if you are predicting house prices and a new house comes on the market, you can predict its sale price.</span></span>

<span data-ttu-id="4fea5-211">因为模型生成器使用自动机器学习 (AutoML)，所以在训练期间不需要任何人工输入或微调操作。</span><span class="sxs-lookup"><span data-stu-id="4fea5-211">Because Model Builder uses automated machine learning (AutoML), it does not require any input or tuning from you during training.</span></span>

### <a name="how-long-should-i-train-for"></a><span data-ttu-id="4fea5-212">训练时长应为多长时间？</span><span class="sxs-lookup"><span data-stu-id="4fea5-212">How long should I train for?</span></span>

<span data-ttu-id="4fea5-213">模型生成器使用 AutoML 浏览多个模型，以查找性能最佳的模型。</span><span class="sxs-lookup"><span data-stu-id="4fea5-213">Model Builder uses AutoML to explore multiple models to find you the best performing model.</span></span>

<span data-ttu-id="4fea5-214">更长的训练周期允许 AutoML 通过更多设置来浏览更多模型。</span><span class="sxs-lookup"><span data-stu-id="4fea5-214">Longer training periods allow AutoML to explore more models with a wider range of settings.</span></span>

<span data-ttu-id="4fea5-215">下表汇总了在本地计算机上为一组示例数据集获取良好性能所花的平均时间。</span><span class="sxs-lookup"><span data-stu-id="4fea5-215">The table below summarizes the average time taken to get good performance for a suite of example datasets, on a local machine.</span></span>

|<span data-ttu-id="4fea5-216">数据集大小</span><span class="sxs-lookup"><span data-stu-id="4fea5-216">Dataset size</span></span>|<span data-ttu-id="4fea5-217">训练的平均时间</span><span class="sxs-lookup"><span data-stu-id="4fea5-217">Average time to train</span></span>|
|------------|---------------------|
|<span data-ttu-id="4fea5-218">0 - 10 MB</span><span class="sxs-lookup"><span data-stu-id="4fea5-218">0 - 10 MB</span></span>|<span data-ttu-id="4fea5-219">10 秒</span><span class="sxs-lookup"><span data-stu-id="4fea5-219">10 sec</span></span>|
|<span data-ttu-id="4fea5-220">10 - 100 MB</span><span class="sxs-lookup"><span data-stu-id="4fea5-220">10 - 100 MB</span></span>|<span data-ttu-id="4fea5-221">10 分钟</span><span class="sxs-lookup"><span data-stu-id="4fea5-221">10 min</span></span>|
|<span data-ttu-id="4fea5-222">100 - 500 MB</span><span class="sxs-lookup"><span data-stu-id="4fea5-222">100 - 500 MB</span></span>|<span data-ttu-id="4fea5-223">30 分钟</span><span class="sxs-lookup"><span data-stu-id="4fea5-223">30 min</span></span>|
|<span data-ttu-id="4fea5-224">500 - 1 GB</span><span class="sxs-lookup"><span data-stu-id="4fea5-224">500 - 1 GB</span></span>|<span data-ttu-id="4fea5-225">60 分钟</span><span class="sxs-lookup"><span data-stu-id="4fea5-225">60 min</span></span>|
|<span data-ttu-id="4fea5-226">1 GB 以上</span><span class="sxs-lookup"><span data-stu-id="4fea5-226">1 GB+</span></span>|<span data-ttu-id="4fea5-227">3 小时以上</span><span class="sxs-lookup"><span data-stu-id="4fea5-227">3+ hours</span></span>|

<span data-ttu-id="4fea5-228">这些数字仅用于指南。</span><span class="sxs-lookup"><span data-stu-id="4fea5-228">These numbers are a guide only.</span></span> <span data-ttu-id="4fea5-229">训练的确切长度取决于：</span><span class="sxs-lookup"><span data-stu-id="4fea5-229">The exact length of training is dependent on:</span></span>

- <span data-ttu-id="4fea5-230">用作模型输入的特征（列）数</span><span class="sxs-lookup"><span data-stu-id="4fea5-230">the number of features (columns) being used to as input to the model</span></span>
- <span data-ttu-id="4fea5-231">列的类型</span><span class="sxs-lookup"><span data-stu-id="4fea5-231">the type of columns</span></span>
- <span data-ttu-id="4fea5-232">ML 任务</span><span class="sxs-lookup"><span data-stu-id="4fea5-232">the ML task</span></span>
- <span data-ttu-id="4fea5-233">用于训练的计算机的 CPU、磁盘和内存性能</span><span class="sxs-lookup"><span data-stu-id="4fea5-233">the CPU, disk, and memory performance of the machine used for training</span></span>

<span data-ttu-id="4fea5-234">通常建议使用的数据集超过 100 行，因为数据集少于 100 行可能不会生成任何结果，并且可能需要花费更长的时间进行训练。</span><span class="sxs-lookup"><span data-stu-id="4fea5-234">It's generally advised that you use more than 100 rows as datasets with less than that may not produce any results and may take a significantly longer time to train.</span></span>

## <a name="evaluate"></a><span data-ttu-id="4fea5-235">评估</span><span class="sxs-lookup"><span data-stu-id="4fea5-235">Evaluate</span></span>

<span data-ttu-id="4fea5-236">评估是衡量模型品质的过程。</span><span class="sxs-lookup"><span data-stu-id="4fea5-236">Evaluation is the process of measuring how good your model is.</span></span> <span data-ttu-id="4fea5-237">模型生成器使用经过训练的模型对新的测试数据进行预测，然后度量预测效果的过程。</span><span class="sxs-lookup"><span data-stu-id="4fea5-237">Model Builder uses the trained model to make predictions with new test data, and then measures how good the predictions are.</span></span>

<span data-ttu-id="4fea5-238">模型生成器将训练数据拆分为训练集和测试集。</span><span class="sxs-lookup"><span data-stu-id="4fea5-238">Model Builder splits the training data into a training set and a test set.</span></span> <span data-ttu-id="4fea5-239">训练数据 (80%) 用于训练模型，测试数据 (20%) 用于评估模型。</span><span class="sxs-lookup"><span data-stu-id="4fea5-239">The training data (80%) is used to train your model and the test data (20%) is held back to evaluate your model.</span></span>

### <a name="how-do-i-understand-my-model-performance"></a><span data-ttu-id="4fea5-240">如何了解模型性能？</span><span class="sxs-lookup"><span data-stu-id="4fea5-240">How do I understand my model performance?</span></span>

<span data-ttu-id="4fea5-241">方案映射到机器学习任务。</span><span class="sxs-lookup"><span data-stu-id="4fea5-241">A scenario maps to a machine learning task.</span></span> <span data-ttu-id="4fea5-242">每个 ML 任务都有其自己的一组评估指标。</span><span class="sxs-lookup"><span data-stu-id="4fea5-242">Each ML task has its own set of evaluation metrics.</span></span>

#### <a name="value-prediction"></a><span data-ttu-id="4fea5-243">值预测</span><span class="sxs-lookup"><span data-stu-id="4fea5-243">Value prediction</span></span>

<span data-ttu-id="4fea5-244">值预测问题的默认指标为 RSquared，RSquared 值的范围介于 0 和 1 之间。</span><span class="sxs-lookup"><span data-stu-id="4fea5-244">The default metric for value prediction problems is RSquared, the value of RSquared ranges between 0 and 1.</span></span> <span data-ttu-id="4fea5-245">1 是可能的最大值，换句话说，RSquared 的值越接近 1，模型的性能就越好。</span><span class="sxs-lookup"><span data-stu-id="4fea5-245">1 is the best possible value or in other words the closer the value of RSquared to 1 the better your model is performing.</span></span>

<span data-ttu-id="4fea5-246">报告的其他指标（如绝对损失、平方损失和 RMS 损失）为附加指标，可以用来理解模型的性能，并将其与其他值预测模型进行比较。</span><span class="sxs-lookup"><span data-stu-id="4fea5-246">Other metrics reported such as absolute-loss, squared-loss, and RMS loss are additional metrics, which can be used to understand how your model is performing and comparing it against other value prediction models.</span></span>

#### <a name="classification-2-categories"></a><span data-ttu-id="4fea5-247">分类（2 个类）</span><span class="sxs-lookup"><span data-stu-id="4fea5-247">Classification (2 categories)</span></span>

<span data-ttu-id="4fea5-248">分类问题的默认指标是“准确性”。</span><span class="sxs-lookup"><span data-stu-id="4fea5-248">The default metric for classification problems is accuracy.</span></span> <span data-ttu-id="4fea5-249">准确性定义的是模型对测试数据集做出的正确预测的比例。</span><span class="sxs-lookup"><span data-stu-id="4fea5-249">Accuracy defines the proportion of correct predictions your model is making over the test dataset.</span></span> <span data-ttu-id="4fea5-250">越接近 100% 或 1.0 越好。</span><span class="sxs-lookup"><span data-stu-id="4fea5-250">The closer to 100% or 1.0 the better it is.</span></span>

<span data-ttu-id="4fea5-251">报告的其他指标，如 AUC（曲线下面积），用于度量真正率和假正率之间的比例，在高于 0.50 时，才是可以接受的模型。</span><span class="sxs-lookup"><span data-stu-id="4fea5-251">Other metrics reported such as AUC (Area under the curve), which measures the true positive rate vs. the false positive rate should be greater than 0.50 for models to be acceptable.</span></span>

<span data-ttu-id="4fea5-252">F1 分数等其他指标可用于控制精准率与召回率之间的平衡。</span><span class="sxs-lookup"><span data-stu-id="4fea5-252">Additional metrics like F1 score can be used to control the balance between Precision and Recall.</span></span>

#### <a name="classification-3-categories"></a><span data-ttu-id="4fea5-253">分类（3 个以上类）</span><span class="sxs-lookup"><span data-stu-id="4fea5-253">Classification (3+ categories)</span></span>

<span data-ttu-id="4fea5-254">多类分类问题的默认指标是微观准确性。</span><span class="sxs-lookup"><span data-stu-id="4fea5-254">The default metric for Multi-class classification is Micro Accuracy.</span></span> <span data-ttu-id="4fea5-255">微观准确性越接近 100% 或 1.0 越好。</span><span class="sxs-lookup"><span data-stu-id="4fea5-255">The closer the Micro Accuracy to 100% or 1.0 the better it is.</span></span>

<span data-ttu-id="4fea5-256">多类分类的另一个重要指标是宏观准确性，类似于微观准确性，越接近 1.0 越好。</span><span class="sxs-lookup"><span data-stu-id="4fea5-256">Another important metric for Multi-class classification is Macro-accuracy, similar to Micro-accuracy the closer to 1.0 the better it is.</span></span> <span data-ttu-id="4fea5-257">考虑这两种准确性类型的一种好方法是：</span><span class="sxs-lookup"><span data-stu-id="4fea5-257">A good way to think about these two types of accuracy is:</span></span>

- <span data-ttu-id="4fea5-258">微观准确性：传入票证分类给正确团队的频率如何？</span><span class="sxs-lookup"><span data-stu-id="4fea5-258">Micro-accuracy: How often does an incoming ticket get classified to the right team?</span></span>
- <span data-ttu-id="4fea5-259">宏观准确性：对于普通团队而言，传入票证符合其业务范围的频率如何？</span><span class="sxs-lookup"><span data-stu-id="4fea5-259">Macro-accuracy: For an average team, how often is an incoming ticket correct for their team?</span></span>

### <a name="more-information-on-evaluation-metrics"></a><span data-ttu-id="4fea5-260">有关评估指标的详细信息</span><span class="sxs-lookup"><span data-stu-id="4fea5-260">More information on evaluation metrics</span></span>

<span data-ttu-id="4fea5-261">有关详细信息，请参阅[模型评估指标](resources/metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="4fea5-261">For more information, see [model evaluation metrics](resources/metrics.md).</span></span>

## <a name="improve"></a><span data-ttu-id="4fea5-262">改进</span><span class="sxs-lookup"><span data-stu-id="4fea5-262">Improve</span></span>

<span data-ttu-id="4fea5-263">如果模型性能评分不符合预期，可以：</span><span class="sxs-lookup"><span data-stu-id="4fea5-263">If your model performance score is not as good as you want it to be, you can:</span></span>

- <span data-ttu-id="4fea5-264">延长训练时间。</span><span class="sxs-lookup"><span data-stu-id="4fea5-264">Train for a longer period of time.</span></span> <span data-ttu-id="4fea5-265">有了更多时间，自动机器学习引擎可以体验更多算法和设置。</span><span class="sxs-lookup"><span data-stu-id="4fea5-265">With more time, the automated machine learning engine experiments with more algorithms and settings.</span></span>

- <span data-ttu-id="4fea5-266">添加更多数据。</span><span class="sxs-lookup"><span data-stu-id="4fea5-266">Add more data.</span></span> <span data-ttu-id="4fea5-267">有时，数据量不足以训练高质量的机器学习模型。对于包含少量示例的数据集，尤其如此。</span><span class="sxs-lookup"><span data-stu-id="4fea5-267">Sometimes the amount of data is not sufficient to train a high-quality machine learning model.This is especially true with datasets that have a small number of examples.</span></span>

- <span data-ttu-id="4fea5-268">均衡分配数据。</span><span class="sxs-lookup"><span data-stu-id="4fea5-268">Balance your data.</span></span> <span data-ttu-id="4fea5-269">对于分类任务，请确保在各个类别间均匀分配训练集。</span><span class="sxs-lookup"><span data-stu-id="4fea5-269">For classification tasks, make sure that the training set is balanced across the categories.</span></span> <span data-ttu-id="4fea5-270">例如，若有四个类别和 100 个训练示例，前两类（标记 1 和标记 2）包含 90 个记录，而剩下两类（标记 3 和标记 4）只包含 10 个记录，这就存在数据不均衡的问题，可能会导致模型很难正确预测标记 3 或标记 4。</span><span class="sxs-lookup"><span data-stu-id="4fea5-270">For example, if you have four classes for 100 training examples, and the two first classes (tag1 and tag2) are used for 90 records, but the other two (tag3 and tag4) are only used on the remaining 10 records, the lack of balanced data may cause your model to struggle to correctly predict tag3 or tag4.</span></span>

## <a name="code"></a><span data-ttu-id="4fea5-271">代码</span><span class="sxs-lookup"><span data-stu-id="4fea5-271">Code</span></span>

<span data-ttu-id="4fea5-272">完成评估阶段后，模型生成器会输出一份模型文件和代码，可以使用该代码将模型添加到应用程序。</span><span class="sxs-lookup"><span data-stu-id="4fea5-272">After the evaluation phase, Model Builder outputs a model file, and code that you can use to add the model to your application.</span></span> <span data-ttu-id="4fea5-273">ML.NET 模型保存为 zip 文件。</span><span class="sxs-lookup"><span data-stu-id="4fea5-273">ML.NET models are saved as a zip file.</span></span> <span data-ttu-id="4fea5-274">用于加载和使用模型的代码会以新项目的形式添加到解决方案中。</span><span class="sxs-lookup"><span data-stu-id="4fea5-274">The code to load and use your model is added as a new project in your solution.</span></span> <span data-ttu-id="4fea5-275">模型生成器还会添加一个示例控制台应用，可以运行该应用来查看工作状态下的模型。</span><span class="sxs-lookup"><span data-stu-id="4fea5-275">Model Builder also adds a sample console app that you can run to see your model in action.</span></span>

<span data-ttu-id="4fea5-276">此外，模型生成器还会输出生成模型的代码，以便你能了解生成模型所使用的步骤。</span><span class="sxs-lookup"><span data-stu-id="4fea5-276">In addition, Model Builder outputs the code that generated the model, so that you can understand the steps used to generate the model.</span></span> <span data-ttu-id="4fea5-277">还可以通过模型训练代码使用新的数据重新训练模型。</span><span class="sxs-lookup"><span data-stu-id="4fea5-277">You can also use the model training code to retrain your model with new data.</span></span>

## <a name="whats-next"></a><span data-ttu-id="4fea5-278">后续步骤</span><span class="sxs-lookup"><span data-stu-id="4fea5-278">What's next?</span></span>

<span data-ttu-id="4fea5-279">[安装](how-to-guides/install-model-builder.md)模型生成器 Visual Studio 扩展</span><span class="sxs-lookup"><span data-stu-id="4fea5-279">[Install](how-to-guides/install-model-builder.md) the Model Builder Visual Studio extension</span></span>

<span data-ttu-id="4fea5-280">请尝试[价格预测或任何回归方案](tutorials/predict-prices-with-model-builder.md)</span><span class="sxs-lookup"><span data-stu-id="4fea5-280">Try [price prediction or any regression scenario](tutorials/predict-prices-with-model-builder.md)</span></span>
