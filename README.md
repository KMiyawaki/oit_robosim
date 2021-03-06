# oit_robosim

[stage_ros](http://wiki.ros.org/stage_ros)を使ったシミュレータ。

## インストール

```shell
$ cd ~/catkin_ws/src
$ git clone https://github.com/KMiyawaki/oit_robosim.git
```

## ロボット一台のシミュレーションデモ

### シンプルなマウステレオペ

```shell
$ roscd oit_robosim/launch/simulation/
$ roslaunch ./simple.launch 
```

RViz と[stage](https://player-stage-manual.readthedocs.io/en/latest/)、[mouse_teleop](https://github.com/ros-teleop/teleop_tools)が起動する。

![2021-01-15_181238.png](./images/2021-01-15_181238.png)

`mouse_teleop`のウィンドウ内をドラッグするとロボットが動く。

![2021-01-15_181004.png](./images/2021-01-15_181004.png)

`roslaunch`を実行した端末で`Ctrl＋C`で全プログラムを終了させる。`mouse_teleop`のウィンドウだけは閉じるボタンで終了させる。

### 地図作成

```shell
$ roscd oit_robosim/launch/simulation/
$ roslaunch ./mapping.launch 
```

前項と同じように`mouse_teleop`のウィンドウ内をドラッグするとロボットが動き、地図が作成される。

### ナビゲーション

```shell
$ roscd oit_robosim/launch/simulation/
$ roslaunch ./navigation.launch 
```

操作方法は[ロボットのナビゲーション](https://github.com/KMiyawaki/lectures/blob/master/ros/stage_simulator/stage_simulator_01.md#%E3%83%AD%E3%83%9C%E3%83%83%E3%83%88%E3%81%AE%E3%83%8A%E3%83%93%E3%82%B2%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3)を参照。

### 画像処理

```shell
$ roscd oit_robosim/launch/simulation/
$ roslaunch ./simple.launch 
```

を実行後、別端末で以下を実行する。

```shell
$ roscd oit_robosim/launch/simulation/
$ roslaunch ./image_proc_sample.launch
```

![2021-01-15_182255.png](./images/2021-01-15_182255.png)

RViz 等に加えて[rqt_image_view](http://wiki.ros.org/rqt_image_view)が開く。`rqt_image_view`に何も表示されていない場合はトピック名選択のドロップボックスから`image_mod`を選ぶ。

実際の画像処理プログラムは`scripts/imaeg_proc_sample.py`にある。

## ロボット二台のシミュレーションデモ

```shell
$ roscd oit_robosim/launch/simulation/
$ roslaunch ./simple_2robots.launch
```

![2021-01-15_182739.png](./images/2021-01-15_182739.png)

２台のロボットとそれぞれの`mouse_teleop`ウィンドウが開き、マウスでロボットを操作できる。

以下のコマンドで`pub/sub`によるロボットの制御ができる。つまりプログラムでコントロールできることを意味する。

```shell
$ rostopic pub /robot_0/cmd_vel geometry_msgs/Twist "linear:
  x: 0.3
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 0.0" -r 10
```

`robot_0`を`robot_1`にすれば別のロボットが走る。
