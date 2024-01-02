[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/lVqgFAye)
[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=13139627&assignment_repo_type=AssignmentRepo)

# Visual Odometry: <br/>

This Project computes Trajectory of the Camera from Stereo and RGBD Images.

**To Install:** OpenCV, Lightglue.

**Test2:** VO on Kitti Dataset. <br />
![Kitti](images/1.png)


**Test3:** Indoor VO using RGDB camera( Lab dataset). <br />
![Lab](images/2.png)

**Test_campus:** VO on Campus data using Zed stereo camera( Self-driving Car dataset). <br />
![Campus](images/3.png)

**Light_glue_test:** VO using Light glue as feature matcher(Kitti dataset). <br />



## Basic Structure:
**Datahandler:** To load Stereo Data from 00 sequence Kitti data. <br />
**Compute Disparity:** Using SGBM and BM functions of CV2 gives us the disparity. compute_left_disparity_map(handler.first_image_left, handler.first_image_right,  matcher='sgbm') <br />
**Stereo_2_depth:** Computes the depth from the above calculated disparity and focal length. <br />
**Visualize_matches():** This calls functions: extract features, match features and filtered matches. Using SIFT, Orb , we match features and then apply a threshold value to filter out the features. <br />
**Estimate Motion:** Here we compute the motion between matched correspondences between frame 1 and 2 and get the rotation and translation using the depth of the matched keypoints. This is done using PNPRANSAC of cv2. <br />
**Visual Odometry():** Here we call all the above functions and store the trajectories from the Transformation matrix calculated from estimated motions function.<br />

# To run the Visual odometry function:<br />

```python
start = datetime.datetime.now()
trajectory_nolidar_bm = visual_odometry(handler,
                                      filter_match_distance=0.8, 
                                      detector='sift',
                                      stereo_matcher='sgbm',
                                      mask=mask,     
                                      subset=None)
end = datetime.datetime.now()
print('Time to perform odometry:', end-start)
```
  
**calculate_error():** Calculates rmse, mae and mse losses.

**Kalman filter:** Applies the Kalman filter on the resultant trajectory.


## Extra functions:

**Light_glue:** It is a deep learning based feature matcher, taking inputs in tensors and returns the data required after converting it to numpy.

# Results:
Depth map for Lab <br />
![Depth map for Lab](images/4.png) <br />
Depth map for Campus <br />
![Depth map for Campus](images/5.png) <br />
Ground Truth vs Estimated Trajectory for Kitti Dataset <br />
![Ground Truth vs Estimated Trajectory for Kitti Dataset](images/6.png) <br />
Kalman Filter <br />
![Kalman Filter](images/7.png) <br />
Estimated Dataset for Campus <br />
![Estimated Dataset for Campus](images/8.png) <br />
Feature Matching from LightGlue <br />
![LightGlue](images/9.png) <br />


**Dataset Link:**
[Dataset link](https://iiitaphyd-my.sharepoint.com/:u:/g/personal/priyansh_sinha_research_iiit_ac_in/EcGJ39mPM0ZGnwW7RPWIpcgBmmKKo-t8CQKbVKY2XEjtxQ?e=MqQjkl) <br />

Feel free to contact us for further clarifications.

**Contributors:** <br /> Priyansh Sinha <br /> Saksham Gupta <br /> Amitabh Sharma.





