# Supervised Machine Learning

* ML systems learn how to combine input to produce useful predictions on never-before-seen data.

### Labels

A label is the thing we're predicting - the y variable in simple linear regression.

### Features

A feature is an input variable - the x variable in simple linear regression. A simple machine learning project might use a single feature, while a more sophisticated machine learning project could use millions of features.

**특성**은 입력 변수입니다(단순 선형 회귀의 `x` 변수). 간단한 머신러닝 프로젝트에서는 특성 하나를 사용하지만 복잡한 머신러닝 프로젝트에서는 다음과 같이 수백만 개의 특성을 사용할 수 있습니다.

### Examples

An example is a particular instance of data, **x**(it is a vector).

*  labeled examples
* unlabeled examples

A labeled example includes both feature(s) and the label.

```
  labeled examples: {features, label}: (x, y)
```

Use labeled examples to **train** the model. In our spam detector example, the labeled examples would be individual emails that users have explicitly marked as "spam" or "not spam."

For example, the following table shows 5 labeled examples from a [data set](https://developers.google.com/machine-learning/crash-course/california-housing-data-description) containing information about housing prices in California:

| housingMedianAge (feature) | totalRooms (feature) | totalBedrooms (feature) | medianHouseValue (label) |
| :------------------------- | :------------------- | :---------------------- | :----------------------- |
| 15                         | 5612                 | 1283                    | 66900                    |
| 19                         | 7650                 | 1901                    | 80100                    |
| 17                         | 720                  | 174                     | 85700                    |
| 14                         | 1501                 | 337                     | 73400                    |
| 20                         | 1454                 | 326                     | 65500                    |

An **unlabeled example** contains features but not the label. That is:

```
  unlabeled examples: {features, ?}: (x, ?)
```

Here are 3 unlabeled examples from the same housing dataset, which exclude `medianHouseValue`:

| housingMedianAge (feature) | totalRooms (feature) | totalBedrooms (feature) |
| :------------------------- | :------------------- | :---------------------- |
| 42                         | 1686                 | 361                     |
| 34                         | 1226                 | 180                     |
| 33                         | 1077                 | 271                     |

Once we've trained our model with labeled examples, we use that model to predict the label on unlabeled examples. In the spam detector, unlabeled examples are new emails that humans haven't yet labeled.

### Models

A model defines the relationship between features and label. For example, a spam detection model might associate certain features strongly with "spam". Let's highlight two phases of a model's life:

- **Training** means creating or **learning** the model. That is, you show the model labeled examples and enable the model to gradually learn the relationships between features and label.
- **Inference**(추론) means applying the trained model to unlabeled examples. That is, you use the trained model to make useful predictions (`y'`). For example, during inference, you can predict `medianHouseValue` for new unlabeled examples.

### Regression vs. classification

A **regression** model predicts continuous values. For example, regression models make predictions that answer questions like the following:

- What is the value of a house in California?
- What is the probability that a user will click on this ad?

A **classification** model predicts discrete(불연속적인) values. For example, classification models make predictions that answer questions like the following:

- Is a given email message spam or not spam?
- Is this an image of a dog, a cat, or a hamster?