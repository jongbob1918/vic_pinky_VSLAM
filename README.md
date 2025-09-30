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
   mkdir -p ~/dev_ws/
   cd ~/dev_ws
   git clone https://github.com/pinklab-art/pinky_violet.git
   ```
3. **의존성 설치**:
   ```bash
   cd ~/vicpinky_ws
   rosdep install --from-paths src --ignore-src -r -y
   ```
4. **빌드**:
   ```bash
   cd ~/vicpinky_ws/src
   colcon build
   ```

### 로봇 설정
1. **패키지 클론**:
   ```bash
   mkdir -p ~/vicpinky_ws/src
   cd ~/vicpinky_ws/src
   git clone https://github.com/pinklab-art/vic_pinky.git
   ```
2. **Gazebo 패키지 삭제**:
   ```bash
   cd vic_pinky
   sudo rm -r vicpinky_gazebo/
   ```
3. **udev 설정**:
   ```bash
   cd ~/vicpinky_ws/src/vic_pinky/doc
   sudo cp ./99-vic-pinky.rules /etc/udev/rules.d/
   sudo udevadm control --reload-rules
   sudo udevadm trigger
   ```
4. **빌드 및 환경 설정**:
   ```bash
   colcon build
   echo 'source ~/vicpinky_ws/install/setup.bash' >> ~/.bashrc
   source ~/.bashrc
   ```

---

## 3. 사용 방법

### SLAM 실행
1. **로봇 실행**:
   ```bash
   ros2 launch vicpinky_bringup bringup.launch.xml
   ```
2. **SLAM 실행**:
   ```bash
   ros2 launch vicpinky_navigation map_building.launch.xml
   ```
3. **지도 저장**:
   ```bash
   ros2 run nav2_map_server map_saver_cli -f <map_name>
   ```

### Navigation 실행
1. **Navigation2 실행**:
   ```bash
   ros2 launch vicpinky_navigation bringup_launch.xml map:=<map_name>
   ```

---

## 4. 시뮬레이션

### Gazebo 실행
1. **Gazebo 실행 및 로봇 스폰**:
   ```bash
   ros2 launch vicpinky_bringup gazebo_bringup.launch.xml
   ```
2. **SLAM 실행 (시뮬레이션)**:
   ```bash
   ros2 launch vicpinky_navigation map_building.launch.xml use_sim_time:=true
   ```
3. **Navigation 실행 (시뮬레이션)**:
   ```bash
   ros2 launch vicpinky_navigation bringup_launch.xml map:=<map_name> use_sim_time:=true
   ```

---

## 5. 이미지

- 아래에 필요한 이미지를 삽입하세요:
  - Gazebo 실행 화면: `<이미지 경로>`
  - RViz Depth 카메라 화면: `<이미지 경로>`

---

이 문서는 간단한 가이드로, 자세한 내용은 각 패키지의 문서를 참고하세요.
