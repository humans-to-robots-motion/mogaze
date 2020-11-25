# Summary

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
```
@article{kratzer2020prediction,
  title={Prediction of Human Full-Body Movements with Motion Optimization and Recurrent Neural Networks},
  author={Kratzer, Philipp and Toussaint, Marc and Mainprice, Jim},
  journal={Robotics and Automation (ICRA), IEEE International Conference on},
  year={2020}
}
```

# Data
The data is available [here](https://ipvs.informatik.uni-stuttgart.de/mlr/philipp/mogaze/).
You can use [this bash script](https://github.com/PhilippJKratzer/mocap-mlr-datasets/blob/master/mogaze.sh) to download all the files using wget.

# Visualization
You can playback the data using the [humoro](https://github.com/PhilippJKratzer/humoro) library.

Here is an example command on how to play participant 1 first file:
```
python3 examples/playback/play_traj.py mogaze/p1_1_human_data.hdf5 --gaze mogaze/p1_1_gaze_data.hdf5 --obj mogaze/p1_1_object_data.hdf5 --segfile mogaze/p1_1_segmentations.hdf5 --scene mogaze/scene.xml
```
