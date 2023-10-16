---
Created: 2023-10-16
tags:
---
# TypeScript에서의 Ambient란 무엇이며 언제 사용하나요?
Ambient는 기본적으로 JavaScript 라이브러리를 TypeScript에서 사용하려 할 때 필요한 타입 정보를 제공하기 위한 방법입니다.
JavaScript는 동적으로 타입이 결정되지만, TypeScript는 정적 타입을 사용하므로 미리 타입 정보를 제공해야 합니다. 이를 위해 Ambient 선언을 사용할 수 있습니다.
`declare` 키워드는 TypeScript에서 외부 코드에 대한 타입 정보를 제공하는 데 중요한 역할을 합니다.
Ambient 선언은 프로젝트 전체에서 사용할 수 있는 전역 변수나 객체에 대한 타입 정보를 제공하는 데 유용하며, 이를 통해 TypeScript는 코드의 타입 안정성을 유지할 수 있습니다.


- **외부 JavaScript 라이브러리 사용**: TypeScript 프로젝트에서 JavaScript 라이브러리를 사용할 때, 해당 라이브러리에 대한 타입 정보를 제공하기 위해 Ambient 선언을 사용합니다.
 - **글로벌 변수 또는 객체 사용**: 프로젝트에서 전역 범위에 있는 변수나 객체를 사용할 때, 이러한 변수나 객체에 대한 타입 정보를 제공하기 위해 Ambient 선언을 사용합니다.

---
# References
1. 