<h1>다이얼로그 플로우로 챗봇 만들기</h1>
<h2>준비</h2>
<p> &nbsp;<a href="https://dialogflow.com/">dialogflow 홈페이지</a>로 들어가서 구글 계정으로 로그인을 한다.
    이후 첫 프로젝트를 만들기 위해 create agent를 해준다.
    Agent의 이름과 사용할 기본 언어(한국어, Korean)를 선택한 뒤 Time zone을 일본, 도쿄 시간으로 설정한다.
    한국, 서울은 도쿄와 동일한 시간대를 사용해서 없는 것같다.
</p>
<h2>Intent란?</h2>
<p> &nbsp;에이전트를 생성했다면 이제 intent를 만들어야한다. intent는 우리의 챗봇의 기능을 뜻한다.
    챗봇을 사용하는 사람이 정보를 검색할 수 있고 예약 같은 프로세스를 처리해달라고 할 수 있다.
    이런 사용자의 요청,의도들을 처리하는 각각의 기능이 intent로 구현된다.
    <br>
    <br>
     &nbsp;우리는 welcome이라는 기본 intent가 있다. 이는 사용자의 다양한 인사에 대한 대답 반응을 모아둔 것이다.
    오른 쪽 영역의 우리가 테스트할 수 있는 곳에 안녕이라고 쳐보면 RESPONSE로 안녕하세요!라는 대답을 해준다.
    intent에는 "안녕?"이라는 것이 등록이 안되어 있고 "안녕"만 있다. 하지만 우리의 dialogflow는 학습을 하기 때문에
    물음표가 붙어있는 안녕 또한 인사 intent가 처리해 주는 것이다.
    <br><br>
     &nbsp;아직 등록되지 않은 하이, 왓썹과 같은 것들에도 반응을 해주고싶다면
    welcome 인텐트의 Training phrases에 해당 구문들을 추가해주면 된다. 
</p>
<h2>식당 예약, Intent 만들기</h2>
<p>
     &nbsp;식당에 예약을 하기 위한 기능을 만든다고 생각해보자. 이 기능을 수행하기 위해서는 별도의 intent가 필요하다.
    add intent를 통해 intent를 하나 만들자. 이름은 Res Reserv 등 편한 것으로 하면된다.
    이후 사용자가 물어보는 구문은 Training phrases에 추가하고
    챗봇의 응답은 RESPONSE에 추가해보자.
    Training phrases에 너무 정확한 구문은 필요하지 않다.
    적절히 추가해주면 챗봇은 학습을 통해 비슷한 질문이 들어오면 알아서 응답을 해주기 때문이다.
    나는 적당히 예약을 하고싶습니다. 예약 가능한가요? 예약하기 를 phrases에 등록했으며
    Response에는 몇시에 예약을 도와드릴까요? 라고 응답하도록 등록했다.
</p>
<p>
     &nbsp;모두 등록을 했으면 왼쪽 메뉴의 Integrations를 눌러 우리가 만든 챗봇을 테스트해보자.
    다양한 툴을 배경으로 테스트를 해볼 수 있다. Web demo의 버튼을 눌러 파란색으로 키면
    주어지는 주소를 브라우저에 입력하여 테스트 사이트로 가보자.
    이후 나오는 채팅창에 우리가 만든 Phrases를 입력하면 챗봇이 Response할 것이다.
</p>
<h2>연계 질의 응답 Intent 만들기</h2>
<p>
     &nbsp;Follow-up Intent를 활용해서 사용자와 챗봇이 연계하여 질의 응답을 하는 기능을 만들어보자.
    이를 통해 사용자가 "예약을 하고싶습니다."라고 물어보면
    챗봇은 "몇시에 예약하시겠습니까?"라고 대답하고 이어서 사용자가 "3시에 하겠습니다."라고 하면
    챗봇이 경우에 따라서 "예약을 진행하겠습니다.", "그 시간에는 예약이 꽉찼습니다." 등을 응답할 수 있다.
</p>
<p>
     &nbsp;Intent 목록에서 우리가 이전에 생성한 Res Reserv에 마우스를 올리면 Add follow-up intent라는 글자가 뜬다.
    이 글자를 누르면 Custom, fallback 등 선택할 수 있는 메뉴가 뜨며 우리는 우리가 Custom할 것이기 때문에
    Custom을 누르면 된다. 그럼 Res Reserv 인텐트 하위에 연계되는 인텐트가 생성된다.
    앞선 Intent에서 챗봇은 몇시에 예약을 도와드릴까요?라고 응답을 하니
    연계 Intent에는 그에 맞는 사용자의 대답을 Training phrases에 등록해주면 된다.
</p>
<h2>단어를 분류하여 응답하는 Intent 만들기</h2>
<p>
     &nbsp;Follow-up Intent를 활용해서 응답을 연계해보았다. 앞에서 까지는 챗봇이 몇시에 예약을 도와드릴까요?
    라고 하는 것까지 했으니 이제 시간을 말하면 그에 따른 응답을 하도록 해보자.
    이를 위해 한번 더 연계하여 Follow up Intent를 만들어야한다.
</p>
<p>
     &nbsp;단어를 구분하기 위해서는 Entity라는 것을 사용해야한다. 연계 Intent를 하나 더 만들었다면 왼쪽 메뉴의 Intent아래의 Entities를 눌러보자
    Intent와 마찬가지고 Entity역시 이름을 정해서 생성하면 된다. 우리는 예약 시간을 정하는 것이기 때문에
    Resvtime이라고 해보자. 이후 아래의 edit entry를 클릭하여 요소를 추가해준다.
    지금은 공부를 하기위한 과정이니 편하게 1시, 2시, 3시만 입력해보자. 추가가 완료되면 SAVE를 해주고 Intent로 들어가
    Training phrases에 1시에 예약할래요. 2시 해줘. 3시가 좋겠어요. 등등 다양한 질의를 등록한 다음 
    1시, 2시, 3시에 각각 마우스로 드래그를 해보자. 사실 드래그를 해보기도 전에 Dialog flow가 알아서
    1시, 2시, 3시라는 글자를 강조하며 아까 만든 Entity의 이름인 Resvtime이라고 표시할 것이다.
</p>
<p>
     &nbsp;이제 챗봇의 Response를 등록해보자. Entity는 $Resvtime라고 적으면 챗봇이 알아서 인식을 한다.
    예를 들어 "정말로 $Resvtime에 예약을 하시겠습니까?" 라는 Response를 등록하면
    사용자가 "1시에 예약할래요."라고 하면 알아서 "정말로 1시에 예약을 하시겠습니까?" 라고 한다.
</p>
<p>
     &nbsp;이제 내가 네. 동의합니다. 그럼요 등등의 응답을 하면 챗봇은 "1시에 예약을 완료했습니다."라고 말해야한다.
    그러기 위해서 연계 Intent를 하나 더 이어서 만들고 Phrases에 동의하는 구문들을 등록해주자.
    이때 "네"라는 Phrases를 등록하면 이 것이 숫자 넷과 관련된 Entity라고 뜨는데 이것은 X버튼을 눌러 삭제해주면 된다.
    이후 Response에서는 바로 "$Resvtime에 예약을 완료했습니다."라고 하면 안된다. 여기의 $Resvtime은 이전 Intent에서
    사용자가 사용한 Entity에 대한 것이 아니기 때문이다. 그렇기 때문에 "#이전Intent이름-followup.Resvtime에 예약을 완료했습니다."라고 응답해줘
    상위 Intent의 Entity를 현재 Intent에서 사용한다고 알려줘야 한다.
</p>
