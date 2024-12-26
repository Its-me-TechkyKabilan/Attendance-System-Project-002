[![Open in Streamlit](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)]
# Attendance-System Using Face-Recognition in Real-Time

## Model Demo

https://user-images.githubusercontent.com/83673888/158333701-9f2cffd8-cd91-496b-98f7-94702bf4bcb6.mp4

## How To Try This Model
There are two versions (Online and Offline) 

|                                 | Online                                         | Offline     |
| --------------------------------| :--------------------------------------------: | :------------------------------------------------------------: |
| Training                        | - Only the host (me) can train new faces.      | - When you clone the repo you can train new faces as you want. |
| Attend from Uploading Photo     | <li>- [x] </li>                                | <li>- [x] </li>                                                |
| Attend from Camera (Photo Mode) | <li>- [x] </li>                                | <li>- [x] </li>                                                |
| Attend Live                     | <li>- [ ] </li>                                | <li>- [x] </li>                                                |

#### **Online Version:** <br>you can try it from [here](https://share.streamlit.io/abdassalamahmad/attendance_system/main/streamlit_test_app_online.py)
#### **Offline Version:** <br>Follow these steps to try it:
1. Clone this repo to get all the code and pre-trained model(pickle_file).
2. Change current directory into the cloned repo folder.
3. Install all of the libraries from [environment.yml] file by using these commands.
```
conda env create -f environment.yml
conda activate attendance
```
(optional step) to check if all libraries installed
```
conda env list
```
4. Install all of the dependencies from [packages.txt] using this command.
  - **Linux users**: cmake is a must.
```
sudo apt-get install cmake libgtk-3-dev freeglut3-dev
```
  - **Windows users**:<br> You need to install visual studio community version from [here](https://visualstudio.microsoft.com/downloads/) and make sure that cmake is checked when installing because it is a must.
5. Run this script [streamlit_local_app_bussines_ready.py]to try the offline version by running this code in the cloned repo directory after installing all dependencies.
```py
streamlit run streamlit_local_app_bussines_ready.py
```

Training :
----------
To train the model on different faces, do the following:
1. Get a photo that contains one person and rename it to the person's name and put it in the `db` folder like this picture.<br>
![image](https://user-images.githubusercontent.com/83673888/158378862-30e4cce9-a737-4079-ae8c-99a013ea7460.png)<br>
2. Repeat that for as many faces as you want.
3. Finally run the [streamlit_local_app_bussines_ready.py] script, and put it on Training mode, and press the `Train The Model` button, then you can go for testing.

Testing :
---------
- You have three modes. The best one is **Live Attendance** (Real case scenario)<br>
To run it do the following:
1. From the sidebar select `Attend Live` mode.
2. Select `Attendance.csv` file, which is a file to record the arrival_time, date, penalty of every attendant.
3. Check `run` box to start the program then show the camera faces of people you've trained (people in `db` folder)

- You can also try attending from uploading a picture of your face and it will work as well.
To run it do the following:
1. From the sidebar select `Attend from uploading image` mode.
2. Upload your image or drag & drop it and it will detect your face and make you attend **just like this picture**.
![image](https://user-images.githubusercontent.com/83673888/158464863-65775d07-0023-4e7e-b15a-f2a09052af35.png)
Note: Of course this is for trying purposes the best model is `Attend Live` described above.



## How This Model Work (what is going on under the hood)
1. Detecting all of the faces in the picture/video:- using HOG algorithm. This function do the work `face_recognition.face_locations`.
2. Transform the face to make the eyes and mouth centered after finding main face landmarks using face landmark estimation.
3. Encode the faces by generating 128 different measuremts per face (saving faces). This function do the training (encodings) `face_recognition.face_encodings`
4. Recognition:- comparing new faces from photo/video with the encoded faces in our dataset. This function `face_recognition.compare_faces` do the comparing and return a list of True and False.
5. Make the attendance :- `markattendance()` this function uses OpenCV library to annotate the faces and then add the name each detected face -based on the previous function return `face_recognition.compare_faces`- 

## Resources and Note
I have used these resources to build my project:
1. [medium article](https://medium.com/@ageitgey/machine-learning-is-fun-part-4-modern-face-recognition-with-deep-learning-c3cffc121d78): -  It descripe in details how **face recognition** is really working under the hood.
2. [YouTube Tutorial](https://www.youtube.com/watch?v=sz25xxF_AVE): - **for attendance part** using OpenCV and HOG. It is basically based on the previous article.
3. I've written the code myself based on the video and enhanced some features like when attending live it was mainly designed to be used for **one day only.**<br>
I changed the logic and make it work **forever**.<br>
I've aslo added the penalty feature for people who are late to work, (they get a 10$ penalty if they came after 9:00 AM).

If you like this project, I appreciate you starring this repo.<br>
Please feel free to fork the content and contact me on my [LinkedIn account](https://www.linkedin.com/in/kabilan-senthilkumar-b35a91287/) if you have any questions.






## To-Do List
- [x] Penalty (10$) for comming late to work (After 9:00 AM).
- [ ] Detect 3D faces only. (printed faces or rendered faces on screens shouldn't be detected).
