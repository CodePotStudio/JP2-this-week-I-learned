# 이번주 리뷰

<br>
TOAST UI Editor for React

리액트에서 사용가능한 무료 WYSIWYG 에디터 라이브러리는 다양하지만
한글 사용에 어려움이 발생하는 경우가 종종 있습니다.
예를 들면, 문서 마지막 글자가 제대로 저장되지 않는 경우 등이 발생합니다.

이러한 문제를 해결하고자 찾던 중
NHN에서 오픈 소스로 공개한 TOAST UI Markdown/WYSIWYG Editor를 알게 되었습니다.
국내에서 개발한 에디터이기에
최소한 한글 지원에 대한 부분은 문제가 없을 것으로 생각되어 선택했습니다.

TOAST UI Editor는 JavaScript, React, Vue를 지원하고 있으며,
리액트에서 사용하고자 한다면, 아래의 패키지를 사용하면 됩니다.
https://github.com/nhn/tui.editor/tree/master/apps/react-editor

사용 방법까지 설명되어 있기에 어렵지않게 사용할 수 있습니다.
다만, Editor에 관한 사용 방법은 명시되어 있으나
함께 사용할 Viewer에 대한 설명은 찾을 수 없습니다.
아마도 Editor와 사용 방법이 동일하기에 별도로 설명하지 않은 듯 합니다.

Viewer를 사용하고자 이리저리 시도한 결과 아래와 같이 사용할 수 있음을 확인했습니다.

import 'codemirror/lib/codemirror.css';
import '@toast-ui/editor/dist/toastui-editor.css';
import { Viewer } from '@toast-ui/react-editor';

const Post = () => {
const content = 'Hello'

    return(
        <>
            <Viewer
                initialValue={ content }
            />
        </>
    )

}

국내 기업인 NHN에서 배포한 오픈소스이지만
웹상에 레퍼런스 자료가 많지 않고
'리액트'에서 'Viewer' 사용에 대한 자료는 더욱 희귀하여
내용을 정리해서 공유합니다.

# 튜터에게 궁금한 점

궁금한점 작성 공간!
