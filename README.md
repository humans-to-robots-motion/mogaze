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
