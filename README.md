<p align="center"><img src="/images/logo_mypt.png"></p>

# 내 손안의 개인 트레이너: MyPT

## <프로젝트 소개>
### &nbsp; 1. 프로젝트 개요 (Overview)

&nbsp; 내 손안의 개인 트레이너, MyP 앱은 인공지능 트레이너 모델을 이용해, 장병들의 운동 자세를 분석하고, 피드백함으로써 운동하는 장병들의 부상을 방지하고, 순위보드를 제공하여 체력 단련을 고취시키는 앱입니다.

## 기능 설명
### &nbsp; 1. 프로젝트 개요 (Overview)
&nbsp; MyPT는 AI를 통해 장병들의 운동자세를 분석해주며, 장병들 사이에 운동 네트워크를 형성해 운동의욕을 고취하는 앱입니다. 또한, 신체 부위 별로 운동하는 법에 대해 설명을 해주어 운동계의 백과사전 역할을 해주는 앱입니다. 군인의 삶에서 체력은 중요 요소입니다. '강인한 육체에 강인한 정신이 깃든다'라는 말처럼, 부대원들의 육체적, 정신적 강인함이 부대의 전투력과 직결됩니다. 저희는 MyPT 인공지능 앱을 개발하여 장병들의 운동자세를 분석해주며 운동 시 부상을 방지하고, 장병들 사이에 운동 네트워크를 형성해 운동의욕을 고취하고자 합니다. MyPT는 관절을 포착하여 특정 관절의 각도가 잘못되었는지, 목표치에 해당하는 운동을 할 때 끝까지 자세가 틀어지지 않는지를 판단하며, 실시간으로 이에 대한 피드백을 음성 지원합니다. 운동이 끝난 뒤, 종합적인 점수를 제공합니다. MyPT 내의 운동 네트워크에는 운동 점수의 랭킹 게시판이 있어 서로 경쟁하며 발전할 수 있습니다.

### &nbsp; 2. 앱의 구성

### &nbsp; 3. PT 서비스
&nbsp; PT를 받기 위해서는 여러분의 준비물은 핸드폰 하나입니다. 간단하죠? MyPT 앱은 푸쉬업(Push up), 풀업(Pull up), 스쿼트(Squat)에 대해 PT 서비스를 제공합니다. 운동을 할 때 카메라를 켜둔 상태로 핸드폰을 오른쪽 측면에 두면 됩니다. 갯수를 세어주고, 사용자의 운동자세를 분석하여 피드백하여줍니다. 예를들어, 푸쉬업의 경우 완전 수축 및 이완을 했는지, 골반이 내려가진 않았는지, 무릎이 내려가지는 않았는지, 속도는 괜찮은지 판단하여 주고 즉각적으로 사용자에게 피드백을 해줍니다. 지금은 이 3가지 운동에 대해서만 서비스를 진행하지만, 향후 더 많은 운동들에 대한 PT가 업데이트 될 것입니다. 저희 팀은 앱 개발을 해커톤 대회에서 멈추지 않고, 계속 개발해 나갈 것입니다. MyPT 앱은 무한한 개발가능성을 가지고 있습니다. Computer Vision을 통해 PT를 서비스를 제공할 수 있다는 가능성을 보여드리기 위해 세가지 운동에 대해서만 코드를 작성하였습니다. 오픈소스인 깃헙을 통해 코드를 공유하여, 저희 팀의 소스 코드를 통해 Computer Vision 분야에서 PT 서비스가 더 발전해 나가면 좋겠습니다.

## 컴퓨터 구성 / 필수 조건 안내


## 기술 스택(Technique Used)
### &nbsp; 1. 프론트 엔드 (Front-End)
### &nbsp; 2. 백엔드 (Back-End)
### &nbsp; 3. AI (인공지능)
&nbsp; AI 분야에서는 ML Kit와 GoogleTTS api를 사용하였습니다.
&nbsp; ML Kit의 Pose Detection model를 매 frame에 적용하여 frame내의 사람의 관절 위치가 어떻게 되는지 3차원 (x,y,z)좌표로 확인합니다.x, y축은 각각 frame의 가로, 세로에 해당하고, z는 깊이(depth, 카메라로부터 얼마나 떨어져있는지)를 나타내는 가상좌표입니다. 양쪽 골반의 중앙의 z값을 0으로 설정하고, 카메라에서 가까워질 수록 z값이 negative(-)한 값이 되며, 멀어질 수록 z값이 postive(+)한 값입니다.
&nbsp; GoogleTTS를 이용해 운동 1회마다 음성으로 사용자가 한 운동의 개수를 알려주며, 3회마다 사용자의 자세에 대한 피드백을 해줍니다.

#### &nbsp; - AI 코드내에 사용된 함수들
&nbsp; utils.dart파일에 자세 분석에 사용되는 함수들이 담겨 있습니다.

<br> findXyz함수는 필요한 관절의 3차원 좌표값 (x,y,z)을 return 합니다.

<br> calculateAngle3D, calculateAngle2D 함수는 벡터사이의 각도를 측정하여 이를 return하는 함수입니다. 벡터의 내적과 외적을 이용하여 측정하는 각도의 방향을 정하고, 측정 방향으로만 각도를 측정합니다. return 하는 운동 각도의 범위는 0°~360°입니다. 두 벡터 사이의 각도는 아래의 사진과 같이 둔각으로도, 예각으로도 표현할 수 있습니다. 
<img src="/images/acute_angle.png"><img src="/images/obtuse_angle.png"></p>
<br> 운동시 관절사이의 각도를 측정하기 위해서는 기준 방향을 설정하여 한 방향으로만 측정을 하여야합니다. 허나 내적이나, actan를 이용하면 벡터사이의 예각만 측정할 수 있습니다. 내적으로 두 벡터사이의 예각을 구한뒤, 두 벡터의 외적의 z성분이 양인지 음인지에 따라 내적의 결과 각도 값이 측정 방향과 같은지, 반대방향인지 판단하여 기준 방향으로만 각도를 측정합니다.

<br> isOutlierPushUps, isOutlierSquats, isOutlierPullups 함수는 Pose Detection이 올바르게 되었는지 판단하여 주는 함수입니다. Pose Detection이 올바르게 되면 true를, 올바르지 않게 되었으면 false를 return합니다. 앱 내에서 실시간으로 매 프레임 별로 자세 분석 시 관절의 위치를 잘못 찍는 노이즈 값들이 간혹 식별되었습니다. 이 노이즈 값들이 자세 평가에 반영이 되지 않도록 하는 함수입니다. 매 frame별로 관찰을 하다가 점을 잘못찍었다고 판단이 되면(관찰하고자하는 관절의 각도의 변화량이 급격하면) 해당 프레임을 무시합니다. 즉, 각도가 연속적으로 변하도록 하는 함수입니다. 운동 종류 및 관절에 따라 프레임별로 변화할 수 있는 threshold를 설정해두고, 각도 변화가 해당 threshold값보다 클 경우 false를 return합니다.
<br><br>
isOutlier함수의 사용 예시입니다.
| Pose detection이 잘 된 경우 | Pose detection이 잘못 된 경우 |
|:---:|:---:|
| ![correct](https://github.com/osamhack2021/AI_APP_MyPT_StrongFriends/blob/main/images/right_pose_detection.jpg?raw=true) | ![wrong](https://github.com/osamhack2021/AI_APP_MyPT_StrongFriends/blob/main/images/wrong_pose_detection.jpg?raw=true) |
| return true | return false |

<br><br>
## 설치 안내 (Installation Process)

## 프로젝트 사용법 (Getting Start)

## 팀 정보

## 저작권 및 사용권 정보 (Copyleft / End User License)
