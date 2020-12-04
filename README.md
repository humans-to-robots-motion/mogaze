This dataset captures long sequences of
full-body everyday manipulation tasks, with eye-gaze.

![sample](https://raw.githubusercontent.com/humans-to-robots-motion/mogaze/master/images/im2.png)

A detailed description can be found on 
[arxiv](https://arxiv.org/abs/2011.11552).

The motion data was captured using a traditional
motion capture system based on reflective markers.
We additionally captured eye-gaze using a wearable pupil-tracking device. 
The dataset can be used for the design and evaluation
of full-body motion prediction algorithms.
Furthermore, our experiments shows eye-gaze as a powerful predictor of human intent.
The dataset includes 180 min of motion capture data with
1627 pick and place actions being performed.

# Citation

When using this dataset please mention the following paper in your work
```bibtex
@article{kratzer2020mogaze,
  title={MoGaze: A Dataset of Full-Body Motions that Includes Workspace Geometry and Eye-Gaze},
  author={Kratzer, Philipp and Bihlmaier, Simon and Balachandra Midlagajni, Niteesh and Prakash, Rohit and Toussaint, Marc and Mainprice, Jim},
  journal={IEEE Robotics and Automation Letters (RAL)},
  year={2020}
}
```

# Data
The data is available [here](https://ipvs.informatik.uni-stuttgart.de/mlr/philipp/mogaze/).
A [single zip file](https://ipvs.informatik.uni-stuttgart.de/mlr/philipp/mogaze/mogaze.zip) with the data can be downloaded:
```bash
wget https://ipvs.informatik.uni-stuttgart.de/mlr/philipp/mogaze/mogaze.zip
```


# Getting Started
You can playback the data using the [humoro](https://github.com/PhilippJKratzer/humoro) library.

Here is a tutorial on getting started with it: [Getting Started](getting_started)

# Visualization

To just visualize the datafiles, you can use the play\_traj.py example. For instance, the following command plays the first file of participant one:
```python
python3 examples/playback/play_traj.py mogaze/p1_1_human_data.hdf5 --gaze mogaze/p1_1_gaze_data.hdf5 --obj mogaze/p1_1_object_data.hdf5 --segfile mogaze/p1_1_segmentations.hdf5 --scene mogaze/scene.xml
```
