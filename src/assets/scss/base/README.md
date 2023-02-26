# Base

프로젝트 전반에 적용되는 스타일 초기화하는 역할을 하는 scss 폴더
(왠만해선 @extend 해서 사용하지 않도록 조심 ->
컴포넌트 별 중첩되어서 성능 이슈 발생, 클래스에서 바로 사용 혹은 mixins에서 정의 후 @include사용 권장)

- `reset.scss`: 브라우저마다 다르게 갖고 있는 기본 스타일을 동일하게 맞추기 위한 scss
- `typograhph.scss`: 프로젝트에서 사용할 font-face를 정의하는 scss
- `helpers.scss`: 간격이나 배치 등 컴포넌트나 HTML element를 컨트롤하는 클래스를 정의한 scss
