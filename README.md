# Pedestrian-Detector

-- Work in progress --

Pedestrian Detector using the TensorFlow Object Detection API and Nanonets.

<p align="center">
  <img src="/output.gif" alt="Pedestrian Detector in action"></img>
</p>

This repo provides complementary material to this [blog post](#target), which compares the performance of four object detectors for a pedestrian detection task. It also introduces a feature to use multiple GPUs in parallel for inference using the multiprocessing package. The count accuracy and FPS for different models (using 1,2,4 or 8 GPUs in parallel) were calculated and plotted.

## Dataset
The [TownCentre](http://www.robots.ox.ac.uk/ActiveVision/Research/Projects/2009bbenfold_headpose/project.html#datasets) dataset is used for training our pedestrian detector. You can use the following commands to download the dataset. This automatically extracts the frames from the video, and creates XML files from the csv groundtruth. The image dimensions are downscaled by a factor of 2 to reduce processing overhead.
```
wget http://www.robots.ox.ac.uk/ActiveVision/Research/Projects/2009bbenfold_headpose/Datasets/TownCentreXVID.avi
wget http://www.robots.ox.ac.uk/ActiveVision/Research/Projects/2009bbenfold_headpose/Datasets/TownCentre-groundtruth.top
python extract_towncentre.py
python extract_GT.py
```
## Setup
### 1. For TensorFlow Object Detection API
Refer to the instructions in this [blog post](#target).

### 2. For Nanonets
**Step 1: Clone the repo**
```
git clone https://github.com/NanoNets/object-detection-sample-python.git
cd object-detection-sample-python
sudo pip install requests
```
**Step 2: Get your free API Key**

Get your free API Key from http://app.nanonets.com/user/api_key

**Step 3: Set the API key as an Environment Variable**
```
export NANONETS_API_KEY=YOUR_API_KEY_GOES_HERE
```
**Step 4: Create a New Model**
```
python ./code/create-model.py
```
>**Note:** An environment variable NANONETS_MODEL_ID will be created in the previous step, with your model ID.

**Step 5: Upload the Training Data**

Place the training data in a folder named `images` and annotations in `annotations/json`
```
python ./code/upload-training.py
```
**Step 6: Train the Model**
```
python ./code/train-model.py
```
**Step 7: Get Model State**

The model takes ~2 hours to train. You will get an email once the model is trained. In the meanwhile you check the state of the model
```
python ./code/model-state.py
```
**Step 8: Make Predictions**

Create a folder named 'test_images' inside the 'nanonets' folder. Place the input images in this folder, and then run this command.
```
python ./code/prediction.py
```

## Results

## Notes
