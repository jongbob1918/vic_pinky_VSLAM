# Vic Pinky VSLAM

Vic Pinky를 활용하여 Depth 카메라와 RTAB-Map SLAM을 구현한 프로젝트입니다. 이 문서는 설치, 실행 방법, 그리고 시뮬레이션에 대한 간단한 가이드를 제공합니다.

---

## 1. 프로젝트 소개

Vic Pinky는 ROS2 기반의 로봇 플랫폼으로, 본 프로젝트에서는 Depth 카메라를 추가하고 RTAB-Map SLAM을 활용하여 실시간 지도 작성 및 자율 주행을 구현합니다.

---

## 2. 설치 및 빌드

### PC 설정
1. **환경**: Ubuntu 24.04, ROS2 Jazzy
2. **패키지 클론**:
   ```bash
   mkdir -p ~/dev_ws
   cd ~/dev_ws
   git clone git@github.com:jongbob1918/vic_pinky_VSLAM.git
   ```
3. **의존성 설치**:
   ```bash
   cd vicpinky_VSLAM
   rosdep install --from-paths src --ignore-src -r -y
   ```
4. **빌드**:
   ```bash
   cd vicpinky_VSLAM
   colcon build
   source ./istall/setup.bash
   ```


## 2. 사용 방법

### SLAM 실행
1. **로봇 실행**:
   ```bash
   ros2 launch vicpinky_bringup bringup.launch.xml use_sim_time:=True
   ```
2. **SLAM 실행**:
다른 터미널 열기
   ```bash
   source ./istall/setup.bash
   ros2 launch vicpinky_navigation rtabmap_only.launch.xml
   ```
   
3. **rviz  실행**:
다른 터미널 열기
   ```bash
   source ./istall/setup.bash
   rviz2
   ```

4. **키보드 조작 실행**:
다른 터미널 열기
   ```bash
   source ./istall/setup.bash
   ros2 run teleop_twist_keyboard teleop_twist_keyboard 
   
   ```

### 키보드 조작 안내 표

| 키 | 동작 |
|----|------|
| `u` | 좌측 상단 이동 |
| `i` | 전진 |
| `o` | 우측 상단 이동 |
| `j` | 좌측 이동 |
| `k` | 정지 |
| `l` | 우측 이동 |
| `m` | 좌측 하단 이동 |
| `,` | 후진 |
| `.` | 우측 하단 이동 |
| `t` | 위로 이동 (+z) |
| `b` | 아래로 이동 (-z) |
| `q`/`z` | 최대 속도 증가/감소 (10%) |
| `w`/`x` | 직진 속도만 증가/감소 (10%) |
| `e`/`c` | 회전 속도만 증가/감소 (10%) |

**Holonomic 모드 (스트레이프 이동)**: Shift 키를 누른 상태에서 위의 키를 사용하세요.

   
5. **지도 저장**:
다른 터미널 열기
   ```bash
   ros2 run nav2_map_server map_saver_cli -f <map_name>
   ```

### Navigation 실행
1. **Navigation2 실행**:
   ```bash
   ros2 launch vicpinky_navigation bringup_launch.xml map:=<map_name>
   ```

---
### 맵변경시 
cd vic_pinky_VSLAM/src/vicpinky_gazebo/launch/launch_sim.launch.xml
code .
'''
<arg name="world_name" default="factory_L1.world"/>
해당 부분을 (addinedu_map.world, factory_L1.world,empty.world ) 중 하나로 변경 하고 

터미널에서
colcon build
source ./install/setup.bash
'''


## 4. 시뮬레이션

### Gazebo 실행
1. **Gazebo 실행 및 로봇 스폰**:
   ```bash
   ros2 launch vicpinky_bringup gazebo_bringup.launch.xml
   ```
2. **SLAM 실행 (시뮬레이션)**:
   ```bash
    ros2 launch vicpinky_navigation rtabmap_only.launch.xml
   ```
3. **Navigation 실행 (시뮬레이션)**:
   ```bash
   ros2 launch vicpinky_navigation bringup_launch.xml map:=<map_name> use_sim_time:=true
   ```

---

