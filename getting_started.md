# Getting started: Display MoGaze data with humoro
This tutorial describes how to get started using the [MoGaze dataset](https://humans-to-robots-motion.github.io/mogaze/) with our pybullet based library [humoro](https://github.com/PhilippJKratzer/humoro).

There is an [ipython notebook version](https://github.com/PhilippJKratzer/humoro/blob/master/examples/getting_started.ipynb) of this tutorial available.

## Installation
The installation is tested on Ubuntu 18.04.

Clone the repository:
```bash
git clone https://github.com/PhilippJKratzer/humoro.git
```

The requirements can be installed using:
```bash
cd humoro
python -m pip install -r requirements.txt
```
    
Finally, you can install humoro system-wide using:
```bash
sudo python3 setup.py install
```

Download the dataset files:
```bash
wget https://ipvs.informatik.uni-stuttgart.de/mlr/philipp/mogaze/mogaze.zip
unzip mogaze.zip
```

## Playback Human data
Let's first have a closer look into the human data only. We can load a trajectory from file using the following:

```python
from humoro.trajectory import Trajectory

full_traj = Trajectory()
full_traj.loadTrajHDF5("mogaze/p1_1_human_data.hdf5")
```

The trajectory contains a data array, a description of the joints and some fixed joints for scaling:

```python
print("The data has dimension timeframe, state_size:")
print(full_traj.data.shape)
print("")
print("This is a list of jointnames (from the urdf) corresponding to the state dimensions:")
print(list(full_traj.description))
print("")
print("Some joints are used for scaling the human and do not change over time")
print("They are available in a dictionary:")
print(full_traj.data_fixed)
```

To play the trajectory using the pybullet player, we spawn a human and add a trajectory to the human
```python
from humoro.player_pybullet import Player
pp = Player()
pp.spawnHuman("Human1")
pp.addPlaybackTraj(full_traj, "Human1")
```

A specific frame can be displayed:
```python
pp.showFrame(3000)
```

Or a sequence of frames can be played using:
```python
pp.play(duration=360, startframe=3000)
```
There is also a possibility to use a Qt5 widget (pp.play_controls()) to allow fast forward and skipping through the file. It has also some options for segmenting the data. We explain it in the segmentation section.

## Playback multiple humans at the same time
Often it is useful to display multiple human trajectories at the same time. For example, it can be used to show the output of a prediction and the ground truth at the same time. 

It can be achieved by spawning a second human and adding a trajectory to it. A trajectory also has an element *startframe*, which tells the player when a trajectory starts.


```python
pp.spawnHuman("Human2", color=[0., 1., 0., 1.])
# this extracts a subtrajectory from the full trajectory:
sub_traj = full_traj.subTraj(3000, 3360)
# we change the startframe of the sub_traj,
# thus the player will play it at a different time:
sub_traj.startframe = 4000
pp.addPlaybackTraj(sub_traj, "Human2")
pp.play(duration=360, startframe=4000)
```

## Loading Objects
There is a helper function to directly spawn the objects and add the playback trajectories to the player:
```python
from humoro.load_scenes import autoload_objects
obj_trajs, obj_names = autoload_objects(pp, "mogaze/p1_1_object_data.hdf5", "mogaze/scene.xml")
pp.play(duration=360, startframe=3000)
```

You can access the object trajectories and names:
```python
print("objects:")
print(obj_names)
print("data shape for first object:")
print(obj_trajs[0].data.shape)  # 7 dimensions: 3 pos + 4 quaternion rotation
```

## Loading Gaze
The gaze can be loaded the following way. Note that only a trajectory of gaze direction points is loaded, the start point comes from the "goggles" object.
```python
from humoro.gaze import load_gaze
gaze_traj = load_gaze("mogaze/p1_1_gaze_data.hdf5")
pp.addPlaybackTrajGaze(gaze_traj)
pp.play(duration=360, startframe=3000)
```

## Segmentations
The following loads a small Qt5 Application that displays a time axis with the segmentations. The file is segmented into when an object moves.

Note that opening the QApplication does not allow to spawn any new objects in pybullet.
```python
pp.play_controls("mogaze/p1_1_segmentations.hdf5")
```

The label "null" means that no object moves at the moment (e.g. when the human moves towards an object to pick it up.

It is also possible to directly use the segmentation file, it contains elements of the form (startframe, endframe, label):
```python
import h5py
with h5py.File("mogaze/p1_1_segmentations.hdf5", "r") as segfile:
    # print first 5 segments:
    for i in range(5):
        print(segfile["segments"][i])
```

## Kinematics
In order to compute positions from the joint angle trajectory, pybullet can be used. We have a small helper class, which can be used like this:
```python
from humoro.kin_pybullet import HumanKin
kinematics = HumanKin()
kinematics.set_state(full_traj, 100)  # set state at frame 100
print("position of right wrist:")
wrist_id = kinematics.inv_index["rWristRotZ"]
pos = kinematics.get_position(wrist_id)
print(pos)
```

The Jacobian can be retreived with:
```python
print(kinematics.get_jacobian(wrist_id))
```
