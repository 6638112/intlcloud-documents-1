

다중 AZ(Available Zone)는 [COS](https://www.tencentcloud.com/products/cos)에서 제공하는 다중 AZ 스토리지 아키텍처를 말하며, 데이터에 대한 IDC 수준의 재해 복구 기능을 제공할 수 있습니다.

귀하의 데이터는 한 리전의 여러 IDC에 분산되어 있습니다. 자연 재해나 정전과 같은 극한 상황으로 인해 IDC가 실패하더라도 다중 AZ 스토리지 아키텍처는 여전히 안정적이고 신뢰할 수 있는 스토리지 서비스를 제공할 수 있습니다.

다중 AZ는 99.9999999999%(12개 9) 설계 데이터 안정성과 99.995% 설계 서비스 가용성을 제공합니다. COS에 데이터 객체를 업로드할 때 스토리지 클래스를 지정하기만 하면 다중 AZ 리전에 저장할 수 있습니다.

> ?
> - 현재 COS의 MAZ 구성은 베이징, 광저우, 상하이 리전에서만 지원되며 향후 다른 퍼블릭 클라우드 리전에서도 사용할 수 있습니다.
> - MAZ 구성을 사용하면 높은 스토리지 요금이 발생합니다. 자세한 내용은 [가격 | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)를 참고하십시오.

## 다중 AZ의 장점

다중 AZ 리전에 데이터를 저장하면 데이터가 여러 청크로 분할되고 해당 코딩 청크는 삭제 코드 알고리즘을 기반으로 계산됩니다. 원본 데이터 청크와 코딩 청크는 혼합되어 스토리지 및 리전 내 재해 복구를 위해 리전의 다른 IDC에 균등하게 배포됩니다. IDC를 사용할 수 없게 되더라도 다른 IDC에서 정상적으로 데이터를 읽거나 쓸 수 있으므로 데이터가 손실 없이 지속적으로 저장되어 비즈니스 데이터 연속성과 고가용성이 유지됩니다. COS 다중 AZ 기능에는 다음과 같은 강점이 있습니다.

- **리전 내 재해 복구**: IDC 간 재해 복구가 지원됩니다. 다중 AZ 스토리지 아키텍처에서 객체 데이터는 동일한 리전의 서로 다른 IDC에 있는 서로 다른 장치에 저장됩니다. IDC가 실패하면 다른 중복 IDC를 계속 사용할 수 있으므로 비즈니스에 영향을 미치지 않고 데이터가 손실되지 않습니다.
- **안정성 및 내구성**: 삭제 코드 기반의 중복 저장 메커니즘을 활용하여 최대 99.9999999999%의 설계 데이터 안정성을 제공합니다. 데이터는 청크로 저장되고 동시에 읽고 쓰여 최대 99.995%의 설계 서비스 가용성을 제공합니다.
- **사용 용이성**: 객체 스토리지 클래스를 지정하여 데이터의 스토리지 아키텍처를 지정할 수 있습니다. 버킷의 객체를 선택하고 다중 AZ 아키텍처에 저장하여 사용하기 더 쉽게 할 수도 있습니다.

다중 AZ 스토리지와 비 다중 AZ 스토리지의 사양 및 제한 사항 비교는 아래와 같습니다.

<table>
<thead>
<tr>
<th>비교 항목</th>
<th>MAZ 스토리지</th>
<th>비 MAZ 스토리지</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap">설계된 데이터 내구성</td>
<td nowrap="nowrap">99.9999999999%  (12개 9)</td>
<td>99.999999999%(11개 9)</td>
</tr>
<tr>
<td>설계된 서비스 가용성</td>
<td>99.995%</td>
<td>99.99%</td>
</tr>
<tr>
<td>지원되는 지역</td>
<td colspan=2><a href="https://intl.cloud.tencent.com/document/product/436/30925">스토리지 클래스 개요</a>를 참고하십시오</td>
</tr>
<tr>
<td nowrap="nowrap">지원되는 스토리지 클래스</td>
<td>MAZ_STANDARD<br>MAZ_STANDARD_IA<br>MAZ_INTELLIGENT_TIERING</td>
<td>STANDARD<br>STANDARD_IA<br>ARCHIVE<br>DEEP ARCHIVE<br>INTELLIGENT TIERING</td>
</tr>
</tbody></table>


## 사용 방법

버킷에 대해 MAZ를 활성화하고 버킷에 업로드된 객체에 대해 객체 스토리지 클래스를 MAZ로 설정할 수 있습니다. 객체를 업로드할 때 객체 스토리지 클래스를 지정하기만 하면 MAZ 스토리지 아키텍처에 저장할 수 있습니다.
즉, 다중 AZ 아키텍처에 파일을 저장하려면 다음 두 단계만 수행하면 됩니다.

1. [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)의 지침에 따라 버킷을 생성하고 **생성 시** MAZ 구성을 활성화합니다.
2. 파일을 업로드하고 업로드 중에 스토리지 클래스를 지정합니다. 파일 업로드 방법에 대한 자세한 내용은 [객체 업로드](https://intl.cloud.tencent.com/document/product/436/13321)를 참고하십시오.

> ?
> - 버킷에 대해 다중 AZ를 활성화하면 비활성화할 수 없으므로 주의해서 활성화하십시오. 다중 AZ는 기본적으로 기존 버킷에 대해 활성화되지 않으며 새 버킷에 대해서만 활성화할 수 있습니다.
> - MAZ 구성이 활성화된 버킷의 경우 객체를 MAZ 스토리지 클래스(MAZ_STANDARD, MAZ_STANDARD_IA 또는 MAZ_INTELLIGENT TIERING)에 업로드할 수 있습니다. 객체를 MAZ_INTELLIGENT TIERING에 업로드하려면 버킷에 대해 인텔리전트 티어링 구성도 활성화해야 합니다.
> - 기존 데이터를 MAZ 버킷에 저장하려면 MAZ를 활성화한 상태에서 버킷을 생성하고 COS Batch의 일괄 복제 기능을 사용하여 기존 버킷의 파일을 새 버킷에 일괄 복제할 수 있습니다. COS Batch 사용 방법에 대한 자세한 내용은 [일괄 작업](https://intl.cloud.tencent.com/document/product/436/32956)을 참고하십시오.

## 사용 제한

현재 COS를 사용하면 MAZ_STANDARD, MAZ_STANDARD_IA 또는 MAZ_INTELLIGENT TIERING 스토리지 클래스에 객체를 업로드할 수 있습니다. 따라서 아래와 같이 스토리지 클래스 변경과 관련된 기능에 대한 제한 사항도 있습니다.

- 스토리지 클래스 제한: 현재 객체는 MAZ 스토리지 클래스(MAZ_STANDARD, MAZ_STANDARD_IA 또는 MAZ_INTELLIGENT TIERING)에만 업로드할 수 있습니다. MAZ_INTELLIGENT TIERING에 객체를 업로드하려면 버킷에 대해 MAZ 구성과 인텔리전트 티어링 구성을 모두 활성화해야 합니다.
- 작업 제한: 현재 객체는 업로드, 다운로드 및 삭제만 가능합니다. 객체는 다중 AZ 버킷에 복제할 수 있지만 단일 AZ 버킷에는 복제할 수 없습니다.
- 라이프사이클 제한: 현재 객체는 만료 시에만 삭제할 수 있지만 MAZ 스토리지 클래스에서 OAZ 스토리지 클래스로 전환할 수 없습니다.
- 리전 간 복제 제한: MAZ 스토리지 클래스에서 OAZ 스토리지 클래스로 객체를 복제할 수 없습니다.

