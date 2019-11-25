---
title: '자습서: 모델 작성기를 사용하여 위생 위반 분류'
description: 이 자습서에서는 ML.NET 모델 작성기를 사용하여 다중 클래스 분류 모델을 빌드하고 샌프란시스코의 식당 위생 위반 심각도를 분류하는 방법을 보여 줍니다.
author: luisquintanilla
ms.author: luquinta
ms.date: 10/30/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: cbe20183d317ac6fe39a937e1cfa8a5e3df81b74
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73977217"
---
# <a name="tutorial-classify-the-severity-of-restaurant-health-violations-with-model-builder"></a><span data-ttu-id="59f01-103">자습서: 모델 작성기를 사용하여 식당 위생 위반의 심각도 분류</span><span class="sxs-lookup"><span data-stu-id="59f01-103">Tutorial: Classify the severity of restaurant health violations with Model Builder</span></span>

<span data-ttu-id="59f01-104">모델 작성기를 사용하여 다중 클래스 분류 모델을 빌드하고 위생 점검 중에 발견된 식당 위생 위험 수준을 분류하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-104">Learn how to build a multiclass classification model using Model Builder to categorize the risk level of restaurant violations found during health inspections.</span></span>

<span data-ttu-id="59f01-105">이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="59f01-106">데이터 준비 및 이해</span><span class="sxs-lookup"><span data-stu-id="59f01-106">Prepare and understand the data</span></span>
> - <span data-ttu-id="59f01-107">시나리오 선택</span><span class="sxs-lookup"><span data-stu-id="59f01-107">Choose a scenario</span></span>
> - <span data-ttu-id="59f01-108">데이터베이스에서 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="59f01-108">Load data from a database</span></span>
> - <span data-ttu-id="59f01-109">모델 학습</span><span class="sxs-lookup"><span data-stu-id="59f01-109">Train the model</span></span>
> - <span data-ttu-id="59f01-110">모델 평가</span><span class="sxs-lookup"><span data-stu-id="59f01-110">Evaluate the model</span></span>
> - <span data-ttu-id="59f01-111">예측에 모델 사용</span><span class="sxs-lookup"><span data-stu-id="59f01-111">Use the model for predictions</span></span>

> [!NOTE]
> <span data-ttu-id="59f01-112">모델 작성기는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-112">Model Builder is currently in Preview.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59f01-113">전제 조건</span><span class="sxs-lookup"><span data-stu-id="59f01-113">Prerequisites</span></span>

<span data-ttu-id="59f01-114">필수 구성 요소 및 설치 지침 목록을 보려면 [모델 작성기 설치 가이드](../how-to-guides/install-model-builder.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="59f01-114">For a list of prerequisites and installation instructions, visit the [Model Builder installation guide](../how-to-guides/install-model-builder.md).</span></span>

## <a name="model-builder-multiclass-classification-overview"></a><span data-ttu-id="59f01-115">모델 작성기 다중 클래스 분류 개요</span><span class="sxs-lookup"><span data-stu-id="59f01-115">Model Builder multiclass classification overview</span></span>

<span data-ttu-id="59f01-116">이 샘플은 모델 작성기로 빌드된 기계 학습 모델을 사용하여 위생 위반 위험을 범주화하는 C# .NET Core 콘솔 애플리케이션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-116">This sample creates a C# .NET Core console application that categorizes the risk of health violations using a machine learning model built with Model Builder.</span></span> <span data-ttu-id="59f01-117">[dotnet/samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/modelbuilder/MulticlassClassification_RestaurantViolations) GitHub 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-117">You can find the source code for this tutorial at the [dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/modelbuilder/MulticlassClassification_RestaurantViolations) GitHub repository.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="59f01-118">콘솔 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="59f01-118">Create a console application</span></span>

1. <span data-ttu-id="59f01-119">"RestaurantViolations"라는 **C# .NET Core 콘솔 애플리케이션**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-119">Create a **C# .NET Core console application** called "RestaurantViolations".</span></span>

## <a name="prepare-and-understand-the-data"></a><span data-ttu-id="59f01-120">데이터 준비 및 이해</span><span class="sxs-lookup"><span data-stu-id="59f01-120">Prepare and understand the data</span></span>

> <span data-ttu-id="59f01-121">기계 학습 모델을 학습하고 평가하는 데 사용되는 데이터 세트는 원래 [San Francisco Department of Public Health Restaurant Safety Scores](https://www.sfdph.org/dph/EH/Food/score/default.asp)(샌프란시스코 공중 보건 식당 안전 점수)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-121">The data set used to train and evaluate the machine learning model is originally from the [San Francisco Department of Public Health Restaurant Safety Scores](https://www.sfdph.org/dph/EH/Food/score/default.asp).</span></span> <span data-ttu-id="59f01-122">편의상 모델을 학습하고 예측하는 데 관련된 열만 포함하도록 데이터 세트를 압축했습니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-122">For convenience, the dataset has been condensed to only include the columns relevant to train the model and make predictions.</span></span> <span data-ttu-id="59f01-123">[데이터 세트](https://data.sfgov.org/Health-and-Social-Services/Restaurant-Scores-LIVES-Standard/pyih-qa8i?row_index=0)에 대해 알아보려면 다음 웹 사이트를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="59f01-123">Visit the following website to learn more about the [dataset](https://data.sfgov.org/Health-and-Social-Services/Restaurant-Scores-LIVES-Standard/pyih-qa8i?row_index=0).</span></span>

<span data-ttu-id="59f01-124">[식당 안전 점수 데이터 세트를 다운로드](https://github.com/luisquintanilla/machinelearning-samples/raw/AB1608219/samples/modelbuilder/MulticlassClassification_RestaurantViolations/RestaurantScores.zip)하고 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-124">[Download the Restaurant Safety Scores dataset](https://github.com/luisquintanilla/machinelearning-samples/raw/AB1608219/samples/modelbuilder/MulticlassClassification_RestaurantViolations/RestaurantScores.zip) and unzip it.</span></span>

<span data-ttu-id="59f01-125">데이터 세트의 각 행에는 위생을 점검하는 동안 관측된 위반에 대한 정보 및 이러한 위반이 공중 보건 및 안전에 미치는 위협에 대한 위험 평가가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-125">Each row in the dataset contains information regarding violations observed during an inspection from the Health Department and a risk assessment of the threat those violations present to public health and safety.</span></span>

| <span data-ttu-id="59f01-126">InspectionType</span><span class="sxs-lookup"><span data-stu-id="59f01-126">InspectionType</span></span> | <span data-ttu-id="59f01-127">ViolationDescription</span><span class="sxs-lookup"><span data-stu-id="59f01-127">ViolationDescription</span></span> | <span data-ttu-id="59f01-128">RiskCategory</span><span class="sxs-lookup"><span data-stu-id="59f01-128">RiskCategory</span></span> |
| --- | --- | --- |
| <span data-ttu-id="59f01-129">루틴 - 예정되지 않음</span><span class="sxs-lookup"><span data-stu-id="59f01-129">Routine - Unscheduled</span></span> | <span data-ttu-id="59f01-130">부적절하게 씻었거나 위생 처리된 식품 접촉 표면</span><span class="sxs-lookup"><span data-stu-id="59f01-130">Inadequately cleaned or sanitized food contact surfaces</span></span> | <span data-ttu-id="59f01-131">위험 수준 보통</span><span class="sxs-lookup"><span data-stu-id="59f01-131">Moderate Risk</span></span> |
| <span data-ttu-id="59f01-132">새 소유권</span><span class="sxs-lookup"><span data-stu-id="59f01-132">New Ownership</span></span> | <span data-ttu-id="59f01-133">고위험 해충 감염</span><span class="sxs-lookup"><span data-stu-id="59f01-133">High risk vermin infestation</span></span> | <span data-ttu-id="59f01-134">위험 수준 높음</span><span class="sxs-lookup"><span data-stu-id="59f01-134">High Risk</span></span> |
| <span data-ttu-id="59f01-135">루틴 - 예정되지 않음</span><span class="sxs-lookup"><span data-stu-id="59f01-135">Routine - Unscheduled</span></span> | <span data-ttu-id="59f01-136">행주가 깨끗하지 않거나 제대로 보관되지 않았거나 살균제가 부적절함</span><span class="sxs-lookup"><span data-stu-id="59f01-136">Wiping cloths not clean or properly stored or inadequate sanitizer</span></span> | <span data-ttu-id="59f01-137">위험 수준 낮음</span><span class="sxs-lookup"><span data-stu-id="59f01-137">Low Risk</span></span> |

- <span data-ttu-id="59f01-138">**InspectionType**: 검사 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-138">**InspectionType**: the type of inspection.</span></span> <span data-ttu-id="59f01-139">새로운 시설에 대한 최초 점검, 정기 점검, 불만 사항 점검 및 기타 여러 유형이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-139">This can either be a first-time inspection for a new establishment, a routine inspection, a complaint inspection, and many other types.</span></span>
- <span data-ttu-id="59f01-140">**ViolationDescription**: 점검 중 발견된 위반에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-140">**ViolationDescription**: a description of the violation found during inspection.</span></span>
- <span data-ttu-id="59f01-141">**RiskCategory**: 위반이 공중 보건 및 안전에 미치는 위험의 심각도입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-141">**RiskCategory**: the risk severity a violation poses to public health and safety.</span></span>

<span data-ttu-id="59f01-142">`label`은 예측할 열입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-142">The `label` is the column you want to predict.</span></span> <span data-ttu-id="59f01-143">분류 작업을 수행하는 경우 목표는 범주(텍스트 또는 숫자)를 할당하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-143">When performing a classification task, the goal is to assign a category (text or numerical).</span></span> <span data-ttu-id="59f01-144">이 분류 시나리오에서 위반의 심각도에는 낮음, 보통 또는 높음 위험 값이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-144">In this classification scenario, the severity of the violation is assigned the value of low, moderate, or high risk.</span></span> <span data-ttu-id="59f01-145">따라서 **RiskCategory**는 레이블입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-145">Therefore, the **RiskCategory** is the label.</span></span> <span data-ttu-id="59f01-146">`features`는 `label` 예측을 위해 모델에 제공하는 입력입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-146">The `features` are the inputs you give the model to predict the `label`.</span></span> <span data-ttu-id="59f01-147">이 경우 **InspectionType** 및 **ViolationDescription**은 **RiskCategory**를 예측하기 위한 기능 또는 입력으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-147">In this case, the **InspectionType** and **ViolationDescription** are used as features or inputs to predict the **RiskCategory**.</span></span>

## <a name="choose-a-scenario"></a><span data-ttu-id="59f01-148">시나리오 선택</span><span class="sxs-lookup"><span data-stu-id="59f01-148">Choose a scenario</span></span>

![Visual Studio의 모델 작성기 마법사](./media/sentiment-analysis-model-builder/model-builder-screen.png)

<span data-ttu-id="59f01-150">모델을 학습하려면 모델 작성기에서 제공하는 사용 가능한 기계 학습 시나리오 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-150">To train your model, select from the list of available machine learning scenarios provided by Model Builder.</span></span> <span data-ttu-id="59f01-151">이 경우 시나리오는 *문제 분류*입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-151">In this case, the scenario is *Issue Classification*.</span></span>

1. <span data-ttu-id="59f01-152">**솔루션 탐색기**에서 *RestaurantViolations* 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **Machine Learning**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-152">In **Solution Explorer**, right-click the *RestaurantViolations* project, and select **Add** > **Machine Learning**.</span></span>
1. <span data-ttu-id="59f01-153">이 샘플의 경우 시나리오는 다중 클래스 분류입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-153">For this sample, the scenario is multiclass classification.</span></span> <span data-ttu-id="59f01-154">모델 작성기의 *시나리오* 단계에서 **문제 분류** 시나리오를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-154">In the *Scenario* step of Model Builder, select the **Issue Classification** scenario.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="59f01-155">데이터 로드</span><span class="sxs-lookup"><span data-stu-id="59f01-155">Load the data</span></span>

<span data-ttu-id="59f01-156">모델 작성기는 SQL Server 데이터베이스 또는 로컬 파일 `csv` 또는 `tsv` 형식에서 데이터를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-156">Model Builder accepts data from a SQL Server database or a local file in `csv` or `tsv` format.</span></span>

1. <span data-ttu-id="59f01-157">모델 작성기 도구의 데이터 단계의 데이터 원본 드롭다운에서 **SQL Server**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-157">In the data step of the Model Builder tool, select **SQL Server** from the data source dropdown.</span></span>
1. <span data-ttu-id="59f01-158">**SQL Server 데이터베이스에 연결** 텍스트 상자 옆에 있는 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-158">Select the button next to the **Connect to SQL Server database** text box.</span></span>
    1. <span data-ttu-id="59f01-159">**데이터 선택** 대화 상자에서 **Microsoft SQL Server 데이터베이스 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-159">In the **Choose Data** dialog, select **Microsoft SQL Server Database File**.</span></span>
    1. <span data-ttu-id="59f01-160">**항상 이 선택 사용** 확인란의 선택을 취소하고 **계속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-160">Uncheck the **Always use this selection** checkbox and select **Continue**.</span></span>
    1. <span data-ttu-id="59f01-161">**연결 속성** 대화 상자에서 **찾아보기**를 선택하고 다운로드한 *RestaurantScores.mdf* 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-161">In the **Connection Properties** dialog, select **Browse** and select the downloaded *RestaurantScores.mdf* file.</span></span>
    1. <span data-ttu-id="59f01-162">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-162">Select **OK**.</span></span>
1. <span data-ttu-id="59f01-163">**테이블 이름** 드롭다운에서 **위반**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-163">Choose **Violations** from the **Table Name** dropdown.</span></span>
1. <span data-ttu-id="59f01-164">**예측할 열(레이블)** 드롭다운에서 **RiskCategory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-164">Choose **RiskCategory** in the **Column to Predict (Label)** dropdown.</span></span>
1. <span data-ttu-id="59f01-165">**입력 열(기능)** 드롭다운에서 선택된 기본 열 선택 항목인 **InspectionType** 및 **ViolationDescription**을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-165">Leave the default column selections, **InspectionType** and **ViolationDescription**, checked in the **Input Columns (Features)** dropdown.</span></span>
1. <span data-ttu-id="59f01-166">**학습** 링크를 선택하여 모델 작성기의 다음 단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-166">Select the **Train** link to move to the next step in Model Builder.</span></span>

## <a name="train-the-model"></a><span data-ttu-id="59f01-167">모델 학습</span><span class="sxs-lookup"><span data-stu-id="59f01-167">Train the model</span></span>

<span data-ttu-id="59f01-168">이 자습서에서 문제 분류 모델을 학습하는 데 사용되는 기계 학습 작업은 다중 클래스 분류입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-168">The machine learning task used to train the issue classification model in this tutorial is multiclass classification.</span></span> <span data-ttu-id="59f01-169">모델 학습 프로세스 중에 모델 작성기는 다른 다중 클래스 분류 알고리즘 및 설정을 통해 개별 모델을 학습하여 데이터 세트에 가장 적합한 모델을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-169">During the model training process, Model Builder trains separate models using different multiclass classification algorithms and settings to find the best performing model for your dataset.</span></span>

<span data-ttu-id="59f01-170">모델을 학습하는 데 필요한 시간은 데이터 양에 비례합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-170">The time required for the model to train is proportional to the amount of data.</span></span> <span data-ttu-id="59f01-171">모델 작성기는 데이터 소스의 크기에 따라 **학습 시간(초)** 의 기본값을 자동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-171">Model Builder automatically selects a default value for **Time to train (seconds)** based on the size of your data source.</span></span>

1. <span data-ttu-id="59f01-172">모델 작성기는 **학습 시간(초)** 값을 10초로 설정하지만 이 값을 30초로 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-172">Although Model Builder sets the value of **Time to train (seconds)** to 10 seconds, increase it to 30 seconds.</span></span> <span data-ttu-id="59f01-173">더 긴 시간 동안 학습하면 모델 작성기가 최상의 모델을 찾아 더 많은 알고리즘과 매개 변수의 조합을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-173">Training for a longer period of time allows Model Builder to explore a larger number of algorithms and combination of parameters in search of the best model.</span></span>
1. <span data-ttu-id="59f01-174">**학습 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-174">Select **Start Training**.</span></span>

    <span data-ttu-id="59f01-175">학습 프로세스 전체에서 진행률 데이터는 학습 단계의 `Progress` 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-175">Throughout the training process, progress data is displayed in the `Progress` section of the train step.</span></span>

    - <span data-ttu-id="59f01-176">**상태**는 학습 프로세스의 완료 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-176">**Status** displays the completion status of the training process.</span></span>
    - <span data-ttu-id="59f01-177">**가장 높은 정확도** 는 모델 작성기가 현재까지 찾은 최고 성능 모델의 정확도를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-177">**Best accuracy** displays the accuracy of the best performing model found by Model Builder so far.</span></span> <span data-ttu-id="59f01-178">더 높은 정확도는 테스트 데이터에서 모델이 더 정확하게 예측된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-178">Higher accuracy means the model predicted more correctly on test data.</span></span>
    - <span data-ttu-id="59f01-179">**최상의 알고리즘** 은 모델 작성기가 현재까지 찾은 최고 성능 알고리즘의 이름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-179">**Best algorithm** displays the name of the best-performing algorithm found by Model Builder so far.</span></span>
    - <span data-ttu-id="59f01-180">**마지막 알고리즘** 은 모델 작성기가 가장 최근에 학습하기 위해 사용한 알고리즘의 이름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-180">**Last algorithm** displays the name of the algorithm most recently used by Model Builder to train the model.</span></span>

1. <span data-ttu-id="59f01-181">학습이 완료되면 **평가** 링크를 선택하여 다음 단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-181">Once training is complete, select the **Evaluate** link to move to the next step.</span></span>

## <a name="evaluate-the-model"></a><span data-ttu-id="59f01-182">모델 평가</span><span class="sxs-lookup"><span data-stu-id="59f01-182">Evaluate the model</span></span>

<span data-ttu-id="59f01-183">학습 단계의 결과는 최상의 성능을 가진 하나의 모델이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-183">The result of the training step is the one model that had the best performance.</span></span> <span data-ttu-id="59f01-184">모델 작성기의 평가 단계에서 출력 섹션에는 **최상의 모델** 항목의 가장 성능이 좋은 모델에서 사용되는 알고리즘과 더불어 **최상의 모델 정확도**의 메트릭이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-184">In the evaluate step of Model Builder, the output section contains the algorithm used by the best performing model in the **Best Model** entry along with metrics in **Best Model Accuracy**.</span></span> <span data-ttu-id="59f01-185">또한 탐색된 모델을 5개까지 포함하는 요약 테이블과 해당 메트릭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-185">Additionally, a summary table containing up to five models that were explored and their metrics is displayed.</span></span>

<span data-ttu-id="59f01-186">정확도 메트릭에 만족하지 않는 경우 모델 정확도를 개선하기 위한 몇 가지 쉬운 방법은 모델을 학습하거나 더 많은 데이터를 사용하기 위한 시간을 늘리는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-186">If you're not satisfied with your accuracy metrics, some easy ways to try to improve model accuracy are to increase the amount of time to train the model or use more data.</span></span> <span data-ttu-id="59f01-187">그렇지 않으면 **코드** 링크를 선택하여 모델 작성기의 최종 단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-187">Otherwise, select the **code** link to move to the final step in Model Builder.</span></span>

## <a name="add-the-code-to-make-predictions"></a><span data-ttu-id="59f01-188">코드를 추가하여 예측하기</span><span class="sxs-lookup"><span data-stu-id="59f01-188">Add the code to make predictions</span></span>

<span data-ttu-id="59f01-189">학습 프로세스의 결과로 두 개의 프로젝트가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-189">Two projects are created as a result of the training process.</span></span>

- <span data-ttu-id="59f01-190">RestaurantViolationsML.ConsoleApp: 모델 학습 및 샘플 소비 코드가 포함된 C# .NET Core 콘솔 애플리케이션입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-190">RestaurantViolationsML.ConsoleApp: A C# .NET Core Console application that contains the model training and sample consumption code.</span></span>
- <span data-ttu-id="59f01-191">RestaurantViolationsML.Model: 입력 및 출력 모델 데이터의 스키마를 정의하는 데이터 모델, 학습 중 가장 성능이 뛰어난 모델의 저장된 버전, 예측을 위한 `ConsumeModel`이라는 도우미 클래스를 포함하는 .NET Standard 클래스 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-191">RestaurantViolationsML.Model: A .NET Standard class library containing the data models that define the schema of input and output model data, the saved version of the best performing model during training, and a helper class called `ConsumeModel` to make predictions.</span></span>

1. <span data-ttu-id="59f01-192">모델 작성기의 코드 단계에서 **프로젝트 추가**를 선택하여 자동 생성된 프로젝트를 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-192">In the code step of Model Builder, select **Add Projects** to add the autogenerated projects to the solution.</span></span>
1. <span data-ttu-id="59f01-193">*RestaurantViolations* 프로젝트에서 *Program.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-193">Open the *Program.cs* file in the *RestaurantViolations* project.</span></span>
1. <span data-ttu-id="59f01-194">*RestaurantViolationsML.Model* 프로젝트를 참조하도록 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-194">Add the following using statement to reference the *RestaurantViolationsML.Model* project:</span></span>

    [!code-csharp [ProgramUsings](~/machinelearning-samples/samples/modelbuilder/MulticlassClassification_RestaurantViolations/RestaurantViolations/Program.cs#L2)]

1. <span data-ttu-id="59f01-195">모델을 사용하여 새 데이터에 대해 예측을 수행하려면 `Main` 메서드 내부에 `ModelInput` 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-195">To make a prediction on new data using the model, create a new instance of the `ModelInput` class inside the `Main` method of your application.</span></span> <span data-ttu-id="59f01-196">위험 범주는 입력에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-196">Notice that the risk category is not part of the input.</span></span> <span data-ttu-id="59f01-197">모델에서 해당 범주를 예측하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-197">This is because the model generates the prediction for it.</span></span>

    [!code-csharp [TestData](~/machinelearning-samples/samples/modelbuilder/MulticlassClassification_RestaurantViolations/RestaurantViolations/Program.cs#L11-L15)]

1. <span data-ttu-id="59f01-198">`ConsumeModel` 클래스의 `Predict` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-198">Use the `Predict` method from the `ConsumeModel` class.</span></span> <span data-ttu-id="59f01-199">`Predict` 메서드는 학습된 모델을 로드하고 모델에 대한 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)을 만든 후 새 데이터에 대해 예측하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-199">The `Predict` method loads the trained model, creates a [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) for the model, and uses it to make predictions on new data.</span></span>

    [!code-csharp [Prediction](~/machinelearning-samples/samples/modelbuilder/MulticlassClassification_RestaurantViolations/RestaurantViolations/Program.cs#L17-L24)]

1. <span data-ttu-id="59f01-200">애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-200">Run the application.</span></span>

    <span data-ttu-id="59f01-201">프로그램에서 생성된 출력은 아래 코드 조각과 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-201">The output generated by the program should look similar to the snippet below:</span></span>

    ```bash
    Inspection Type: Complaint
    Violation Description: Inadequate sewage or wastewater disposal
    Risk Category: Moderate Risk
    ```

<span data-ttu-id="59f01-202">생성된 프로젝트를 나중에 다른 솔루션 내에서 참조해야 하는 경우 `C:\Users\%USERNAME%\AppData\Local\Temp\MLVSTools` 디렉터리 내에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-202">If you need to reference the generated projects at a later time inside of another solution, you can find them inside the `C:\Users\%USERNAME%\AppData\Local\Temp\MLVSTools` directory.</span></span>

<span data-ttu-id="59f01-203">지금까지</span><span class="sxs-lookup"><span data-stu-id="59f01-203">Congratulations!</span></span> <span data-ttu-id="59f01-204">모델 작성기를 사용하여 위생 위반 위험을 범주화하기 위한 기계 학습 모델을 성공적으로 빌드했습니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-204">You've successfully built a machine learning model to categorize the risk of health violations using Model Builder.</span></span> <span data-ttu-id="59f01-205">[dotnet/samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/modelbuilder/MulticlassClassification_RestaurantViolations) GitHub 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f01-205">You can find the source code for this tutorial at the [dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/modelbuilder/MulticlassClassification_RestaurantViolations) GitHub repository.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="59f01-206">추가 자료</span><span class="sxs-lookup"><span data-stu-id="59f01-206">Additional resources</span></span>

<span data-ttu-id="59f01-207">이 자습서에서 언급한 항목에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f01-207">To learn more about topics mentioned in this tutorial, visit the following resources:</span></span>

- [<span data-ttu-id="59f01-208">모델 작성기 시나리오</span><span class="sxs-lookup"><span data-stu-id="59f01-208">Model Builder Scenarios</span></span>](../automate-training-with-model-builder.md#scenarios)
- [<span data-ttu-id="59f01-209">다중 클래스 분류</span><span class="sxs-lookup"><span data-stu-id="59f01-209">Multiclass Classification</span></span>](../resources/glossary.md#multiclass-classification)
- [<span data-ttu-id="59f01-210">다중 클래스 분류 모델 메트릭</span><span class="sxs-lookup"><span data-stu-id="59f01-210">Multiclass Classification Model Metrics</span></span>](../resources/metrics.md#metrics-for-multi-class-classification)