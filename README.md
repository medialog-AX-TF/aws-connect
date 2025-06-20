# AWS Connect 설정 자동화 프로젝트

이 프로젝트는 AWS Connect의 다양한 구성요소(Contact Flows, Queues, Routing Profiles 등)를 JSON 파일로 정의하고, 이를 배포 스크립트를 통해 AWS 환경에 적용하는 것을 목표로 합니다.

## 디렉토리 구조

```
aws-connect-config/
├── contact_flows/
│   ├── inbound_main.json       # 메인 인바운드 콜 흐름
│   ├── recording_flow.json     # 통화 녹음 관련 흐름
│   └── survey_post_call.json   # 통화 후 설문조사 흐름
├── routing_profiles/
│   └── default_routing_profile.json # 기본 라우팅 프로필
├── queues/
│   └── support_queue.json      # 기술 지원 대기열
├── hours_of_operation/
│   └── working_hours_korea.json # 한국 기준 운영 시간
├── phone_numbers/
│   └── did_mapping.json        # DID 번호와 Contact Flow 매핑 정보
├── agents/
│   └── agents_list.csv         # 상담원 목록
├── lambdas/
│   └── function_config.json    # Connect와 연동될 Lambda 함수 설정
└── deploy.sh                   # 배포 스크립트
```

## 사용 방법

1.  **구성 파일 수정**: `aws-connect-config` 디렉토리 하위의 JSON, CSV 파일들을 실제 운영 환경에 맞게 수정합니다.
2.  **배포 스크립트 실행**: `deploy.sh` 스크립트를 실행하여 변경 사항을 AWS 계정에 배포합니다. (스크립트 내부는 AWS CLI 또는 AWS SDK를 사용하는 로직으로 채워져야 합니다.)

## 주요 파일 설명

-   **contact_flows**: 고객 응대 시나리오를 정의하는 파일들이 위치합니다. AWS Connect Contact Flow Export/Import 형식을 따릅니다.
-   **routing_profiles**: 상담원 그룹의 라우팅 방식을 정의합니다.
-   **queues**: 고객 문의가 대기하는 장소인 대기열을 정의합니다.
-   **hours_of_operation**: 업무 시간을 설정합니다.
-   **phone_numbers**: 발급받은 DID 번호를 어떤 Contact Flow로 연결할지 매핑합니다.
-   **agents**: Connect에 등록할 상담원 정보를 관리합니다.
-   **lambdas**: Connect Contact Flow에서 호출하는 AWS Lambda 함수의 정보를 정의합니다.
-   **deploy.sh**: 위의 설정 파일들을 읽어 AWS Connect 리소스를 생성/수정하는 자동화 스크립트입니다.