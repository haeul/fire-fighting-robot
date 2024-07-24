화재 진압 로봇 (2022/11/10 ~ 2022/12/10)

1.		개발 목표와 특징
목표: 사람이 들어가기 힘든 화재 현장에 투입해 화재를 진압할 수 있는 로봇을 만드는 것.
특징: 낭떠러지, 장애물을 피하며 자율주행을 하다가 화재를 탐지하면 화재 방향으로 물을 뿌려 화재를 진압함.

2.		개발 필요성 
사람이 들어가기 힘든 위험한 화재 현장에 투입됐다가 다치거나 순직하는 
소방관이 많기 때문에 대신 들어가서 화재를 진압해줄 로봇이 개발되면 
안타까운 상황들을 막을 수 있기 때문에 필요하다고 생각한다.

3.		H/W 구현 
ABOT에 양면 테이프를 이용해 브레드보드를 붙이고 그 위에 Ir led와 Receiver를 연결하고 서보모터를 양면 테이프로 붙임.
Ir led에는 2k 저항 대신 4.7k 저항을 연결해 조금 더 가까운 것을 감지하게 함.
서보모터에는 박스를 잘라서 만든 판과 양면 테이프를 이용해 초음파센서와 불꽃감지센서를 붙임.
플라스틱 통에 모터드라이버를 붙이고 워터펌프모터를 넣어서 몸체에 양면 테이프로 붙였고 박스를 잘라 만든 발사대로 고무호스를 고정.

![image](https://github.com/user-attachments/assets/2178e5bd-6239-4e13-99b7-9539f76513d4)
![image](https://github.com/user-attachments/assets/5d39082b-7959-42f6-86ff-e7d5e87bb519)
![image](https://github.com/user-attachments/assets/857c9ed6-a052-42a9-bab3-931262cd1880)
![image](https://github.com/user-attachments/assets/bcf491e9-e331-40d4-b654-277adc0d34df)


4.		S/W 구현 
적외선 센서를 이용한 낭떠러지 IR주행 코드를 베이스로 초음파센서, 불꽃감지센서, 서보모터를 활용해
전방 180도(센서 감지 범위 포함)를 탐지해 장애물을 회피하고 불꽃을 감지하게 함.
워터펌프모터는 모터드라이버와 함께 제어해 불꽃을 감지하면 물을 발사하도록 함.

과정을 처음부터 설명해보자면 정지 상태에서 서보모터를 돌려 전방 180도를
탐지하는데 이때 초음파 센서에 의해 왼쪽과 오른쪽에 감지되는 거리를 받고
불꽃감지센서로 화재가 감지되는지 입력 받는다.
만약 불꽃이 감지되면 그 순간 서보모터의 회전각을 받아서 저장하고 몸체를 그 각만큼
회전시키는데 회전하는 기준이 되는 바퀴와 감지하는 센서가 달려있는 서보모터는
거리 차이가 있기 때문에 몸체를 회전시키기 전에 이 차이만큼 전진하도록 했다.

이 과정을 구현하기 위해 서보모터와 두 바퀴중심을 연결한 선 사이의 길이를 측정했고
몸체를 90도 돌리는데 걸리는 시간을 측정해 90으로 나눠 1도 돌리는데 걸리는 시간을 구해 정확한 방향으로 물을 발사할 수 있도록 했다.

주행 중에 적외선 센서를 이용한 낭떠러지 회피 주행을 하다가 20cm 이내에 장애물이 감지됐을 때는 장애물 회피 주행을 한다.
초음파로 탐지한 좌우 거리가 모두 10cm 미만일 때는 벽에 가로막혔다고 판단해 우회전으로 뒤로 돌아 빠져나가고 오른쪽 거리가 왼쪽 거리 이상일 때는 우회전, 반대의 경우 좌회전으로 장애물을 회피하도록 했다.

5.		향후 보완 사항 
센서를 더 늘려서 탐지 범위를 늘려야하고 카메라와 라이트를 달아서 카메라를
통해 밖에서 상황을 볼 수 있게, 그리고 필요시에는 수동으로 조종할 수 있게 
하는 것도 좋을 것 같다.

또 워터펌프 쪽에도 모터를 달아 몸체가 직접 회전할 필요없이 호스를 회전시켜
원하는 방향에 물을 뿌릴 수 있게 해야 한다.



