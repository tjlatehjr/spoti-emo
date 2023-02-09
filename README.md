# spoti-emo

## Music Recommendation Based on Facial Expression Sporify api Python

The emotion recognition model is trained on FER 2013 dataset. It can detect 7 emotions. The project works by getting live video feed from web cam, pass it through the model to get a prediction of emotion. Then according to the emotion predicted, the app will fetch playlist of songs from Spotify through spotipy wrapper and recommend the songs by displaying them on the screen.

## Features:

Real time expression detection and song recommendations.
Playlists fetched from Spotify using API.
Neumorphism UI for website.

## Installation Steps:

Flask:

- Run <code>pip install -r requirements.txt</code> to install all dependencies.
- In Spotipy.py enter your credentials generated by your Spotify Developer account in 'auth_manager'. Note: - This is only required if you want to update recommendation playlists. Also uncomment import statement in 'camera.py'.
- Run <code>python app.py</code> and give camera permission if asked.

## Technology Overview:

1. Keras
2. Tensorflow
3. Spotipy
4. flask
5. Flask

## Dataset:

The dataset used for this project is the famous FER2013 dataset. Models trained on this dataset can classify 7 emotions. The dataset can be found <a href = "https://www.kaggle.com/msambare/fer2013">here</a>.

Note that the dataset is highly imbalanced with happy class having maxiumum representation. This might be a factor resulting in okaysish accuracy after training.

## Model Architecture:

The model architecture is a sequential model consisting of Conv2d, Maxpool2d, Dropout and Dense layers:

1. Conv2D layers throughout the model have different filter size from 32 to 128, all with activation 'relu'
2. Pooling layers have pool size (2,2)
3. Dropout is set to 0.25 as anything above results in poor performance
4. Final Dense layer has 'softmax' activation for classifying 7 emotions
   Used 'categorical_crossentropy' for loss with 'Adam' optimizer with 'accuracy' metric

Note:- Tried Implementing various other models like VGG16 but accuracy was far too low. This model architecture gives good enough accuracy. A bit more tinkering with hyper parameters might lead to a better accuracy

## Image Processing and Training:

The images were normalised, resized to (48,48) and converted to grayscale in batches of 64 with help of 'ImageDataGenerator' in Keras API.
Training took around 13 hours locally for 75 epochs with an accuracy of ~66 %

## Issue:

The app in current state can't be deployed on web as:

1. Opencv tries to open the camera on whatever device the app is running on. Code in current state makes use of webcam if available on server side not client side. So when app is run locally on a laptop Video Streaming through webcam is possible. But if it's deployed to a cloud, the app is stored in a data center somewhere which obviously doesn't have web camera connected to it and hence it doesn't work.

## Further Work:

1. Instead of CSVs, create a databse and connect it to application. The DB will fetch songs for recommendations and new songs can be updated directly onto database
2. Add a feature which will update specified playlists for better and more recent recommendations, a specific day over a fixed duration say every sunday and append it to database
3. Directly play the song or redirect to the song on Spotify when user clicks on it.
4. Rewrite code such that Video Streaming is done on client side instead of server side so as it make the app deployable

Note: Model accuracy is not that great. It is ~66%. Further training and finetuning required. May try Vision Transformer Model.
