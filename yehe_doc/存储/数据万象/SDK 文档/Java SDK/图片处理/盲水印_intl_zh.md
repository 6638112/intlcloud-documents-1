## 简介

本文档提供关于盲水印的 API 概览以及 SDK 示例代码。

| API                                                          | 操作描述                         |
| ------------------------------------------ | -------------------------- |
| [盲水印](https://intl.cloud.tencent.com/document/product/1045/43029) | 对本地图片添加或提取盲水印并上传至存储桶 |

## 添加盲水印

#### 功能说明

盲水印支持在上传时添加以及下载时添加。

#### 示例代码：上传时添加盲水印

[//]: # ".cssg-snippet-put-object-with-watermark"
```java
// bucket名需包含appid
// api 请参考：https://cloud.tencent.com/document/product/436/46782
String bucketName = "examplebucket-1250000000";

String key = "test.png";
File localFile = new File("E://test.png");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
PicOperations picOperations = new PicOperations();
picOperations.setIsPicInfo(1);
List<PicOperations.Rule> ruleList = new LinkedList<>();
PicOperations.Rule rule = new PicOperations.Rule();
rule.setBucket(bucketName);
rule.setFileId("test-watermark.png");
rule.setRule("watermark/3/type/3/text/dGVuY2VudCBjbG91ZA==");
ruleList.add(rule);
picOperations.setRules(ruleList);
putObjectRequest.setPicOperations(picOperations);
try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    CIUploadResult ciUploadResult = putObjectResult.getCiUploadResult();
    System.out.println(putObjectResult.getRequestId());
    System.out.println(ciUploadResult.getOriginalInfo().getEtag());
    for(CIObject ciObject:ciUploadResult.getProcessResults().getObjectList()) {
        System.out.println(ciObject.getLocation());
    }
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```

#### 参数说明

PicOperations 类用于记录图像操作，其主要成员说明如下：

| 成员名称  | 描述                                                         | 类型 |
| --------- | ------------------------------------------------------------ | ---- |
| isPicInfo | 是否返回原图信息，0不返回原图信息，1返回原图信息，默认为0    | int  |
| rules     | 处理规则，一条规则对应一个处理结果（目前支持五条规则），不填则不进行图片处理 | List |

#### 返回参数说明

CIUploadResult 类用于返回图片处理结果信息，其主要成员说明如下：

| 成员名称       | 描述         | 类型           |
| -------------- | ------------ | -------------- |
| originalInfo   | 原图信息     | OriginalInfo   |
| processResults | 图片处理结果 | ProcessResults |

  OriginalInfo 类用于记录原图信息，其主要成员说明如下：

| 成员名称  | 描述                                                       | 类型      |
| --------- | ---------------------------------------------------------- | --------- |
| key       | 原图文件名                                                 | String    |
| location  | 图片路径                                                   | String    |
| imageInfo | 原图图片信息                                               | ImageInfo |


ImageInfo 类用于记录原图图片信息，其主要成员说明如下：

| 成员名称    | 描述         | 类型    |
| ----------- | ------------ | ------- |
| format      | 格式         | String  |
| width       | 图片宽度     | Integer |
| height      | 图片高度     | Integer |
| quality     | 图片质量     | Integer |
| ave         | 图片主色调   | String  |
| orientation | 图片旋转角度 | Integer |

ProcessResults 类用于记录图片处理结果，其主要成员说明如下：

| 成员名称   | 描述               | 类型 |
| ---------- | ------------------ | ---- |
| objectList | 每一个图片处理结果 | List |

CIObject 类用于记录一个图片处理结果，其主要成员说明如下：

| 成员名称       | 描述                       | 类型    |
| -------------- | -------------------------- | ------- |
| key            | 文件名                     | String  |
| location       | 图片路径                   | String  |
| format         | 图片格式                   | String  |
| width          | 图片宽度                   | Integer |
| height         | 图片高度                   | Integer |
| size           | 图片大小                   | Integer |
| quality        | 图片质量                   | Integer |



#### 示例代码：下载时添加盲水印

[//]: # ".cssg-snippet-download-object-with-watermark"
```java
GetObjectRequest getObj = new GetObjectRequest(bucketName, key);
// 这里是盲水印规则，具体请参考数据万象API，这里仅是示例
String rule = "watermark/3/type/3/text/dGVuY2VudCBjbG91ZA==";
getObj.putCustomQueryParameter(rule, null);

cosClient.getObject(getObj);
```


## 提取盲水印

下面示例展示了如何对已添加盲水印的图片提取盲水印。

#### 示例代码

[//]: # ".cssg-snippet-get-object-watermark-status"
```java
String bucketName = "examplebucket-1250000000";
String key = "qrcode-watermark.png";
File localFile = new File("E://qrcode-watermark.png");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
PicOperations picOperations = new PicOperations();
picOperations.setIsPicInfo(1);
List<PicOperations.Rule> ruleList = new LinkedList<>();
PicOperations.Rule rule = new PicOperations.Rule();
rule.setBucket(bucketName);
rule.setFileId("qrcode-watermark-extract.png");
rule.setRule("watermark/4/type/2/image/aHR0cDovL2V4YW1wbGVidWNrZXQtMTI1MDAwMDAwMC5jb3MuYXAtZ3Vhbmd6aG91Lm15cWNsb3VkLmNvbS9zaHVpeWluLnBuZw==");
ruleList.add(rule);
picOperations.setRules(ruleList);
putObjectRequest.setPicOperations(picOperations);
try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    CIUploadResult ciUploadResult = putObjectResult.getCiUploadResult();
    System.out.println(putObjectResult.getRequestId());
    System.out.println(ciUploadResult.getOriginalInfo().getEtag());
    for(CIObject ciObject:ciUploadResult.getProcessResults().getObjectList()) {
        System.out.println(ciObject.getLocation());
        System.out.println(ciObject.getWatermarkStatus());
    }
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
#### 参数说明

PicOperations 类用于记录图像操作，其主要成员说明如下：

| 成员名称  | 描述                                                         | 类型 |
| --------- | ------------------------------------------------------------ | ---- |
| isPicInfo | 是否返回原图信息，0不返回原图信息，1返回原图信息，默认为0    | int  |
| rules     | 处理规则，一条规则对应一个处理结果（目前支持五条规则），不填则不进行图片处理 | List |

#### 返回参数说明

CIUploadResult 类用于返回图片处理结果信息，其主要成员说明如下：

| 成员名称       | 描述         | 类型           |
| -------------- | ------------ | -------------- |
| originalInfo   | 原图信息     | OriginalInfo   |
| processResults | 图片处理结果 | ProcessResults |

  OriginalInfo 类用于记录原图信息，其主要成员说明如下：

| 成员名称  | 描述                                                       | 类型      |
| --------- | ---------------------------------------------------------- | --------- |
| key       | 原图文件名                                                 | String    |
| location  | 图片路径                                                   | String    |
| imageInfo | 原图图片信息                                               | ImageInfo |


ImageInfo 类用于记录原图图片信息，其主要成员说明如下：

| 成员名称    | 描述         | 类型    |
| ----------- | ------------ | ------- |
| format      | 格式         | String  |
| width       | 图片宽度     | Integer |
| height      | 图片高度     | Integer |
| quality     | 图片质量     | Integer |
| ave         | 图片主色调   | String  |
| orientation | 图片旋转角度 | Integer |

ProcessResults 类用于记录图片处理结果，其主要成员说明如下：

| 成员名称   | 描述               | 类型 |
| ---------- | ------------------ | ---- |
| objectList | 每一个图片处理结果 | List |

CIObject 类用于记录一个图片处理结果，其主要成员说明如下：

| 成员名称        | 描述                                                         | 类型    |
| --------------- | ------------------------------------------------------------ | ------- |
| key             | 文件名                                                       | String  |
| location        | 图片路径                                                     | String  |
| format          | 图片格式                                                     | String  |
| width           | 图片宽度                                                     | Integer |
| height          | 图片高度                                                     | Integer |
| size            | 图片大小                                                     | Integer |
| quality         | 图片质量                                                     | Integer |
| watermarkStatus | 当 type 为2时返回该字段，表示提取到全盲水印的可信度。具体为0 - 100的数字，75分以上表示确定有盲水印，60 - 75表示疑似有盲水印，60以下可认为未提取到盲水印 | Integer |
