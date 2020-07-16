# A Human-fullbody Motion Dataset with Gaze

Existing datasets of full-body motion rarely include 
1) long sequences of manipulation tasks
2) the 3D model of the workspace geometry, and 
3) eye-gaze

which are all important when a
robot needs to predict the movements of humans in close proximity.
Hence, in this novel dataset of full-body
motion for everyday manipulation task,
which includes the above.


The motion data was captured using a traditional
motion capture system based on reflective markers.
We additionally captured eye-gaze using a wearable pupil-tracking device. 
As we show in experiments, the dataset can be used for the design and evaluation
of full-body motion prediction algorithms.
Furthermore, our experiments shows eye-gaze as a powerful predictor of human intent.
The dataset includes 180 min of motion capture data with
1627 pick and place actions being performed.

# Data
The data is available [here](https://ipvs.informatik.uni-stuttgart.de/mlr/philipp/mogaze/).
You can use [this bash script](https://github.com/PhilippJKratzer/mocap-mlr-datasets/blob/master/mogaze.sh) to download all the files using wget.

# Visualization
You can playback the data using the [humoro](https://github.com/PhilippJKratzer/humoro) library.

Here is an example command on how to play participant 1 first file:
```
python3 examples/playback/play_traj.py mogaze/p1_1_human_data.hdf5 --gaze mogaze/p1_1_gaze_data.hdf5 --obj mogaze/p1_1_object_data.hdf5 --segfile mogaze/p1_1_segmentations.hdf5 --scene mogaze/scene.xml
```

![sample](https://raw.githubusercontent.com/humans-to-robots-motion/mogaze/master/images/im2.png)
