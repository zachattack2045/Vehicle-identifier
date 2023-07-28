# Vehicle-identifier

This model is used to identify different vehicles that could be dangerous to interact with on the streets. 

## The Algorithm
This algorithm is used by training an AI model to find colors, patterns, and ethics to know the difference between multiple vehicles. This started by training it to recognize the difference between a car and a motorcycle but could easily be trained to identify ambulances, police cars, and firetrucks to have automotive vehicles avoid them.  
Note: I ran this model on a realivly low epoch with information that was a miniscule amount because I had to make my own dataset. The pretrained model is quite inacurrate.
## Running this project

1. Connect to your Jetson Nano via VSCODE. 
2. Make a folder inside Jetson-inference/python/training/sclassification/data called vehicles and make a folder called "car_motorcycle" and a file called "labels.txt
   that has the words car and motorcycle on different lines
3. in the car_motorcycle file create three different folders called test, train, and val. And finally inside these add folders called car and motorcycle. This is where u will put your images.
4. Since using the preflashed SD card, there sould be a docker container. This is accesable by implementing this code. Change directories into jetson-inference. - use this code if your in the home.$ cd jetson-inference
5. Then run this code -$ ./docker/run.sh the code moves the final-projects folder into the docker container so that the images from vs code are there
6a. Then change directories to jetson-inference/python/training/classification. Paste the following code - $ python3 train.py --model-dir=models/car_motorcycle data/car_motorcycle
6b. your model should be training pretty quickly so when its done run this code in the docker to export it.python3 onnx_export.py --model-dir=models/car_motorcycle.
7. exit the docker by typing exit or pressing ctrl + d and cd python/training/classification run the two lines of code:NET=models/car_motorcycle and DATASET=data/car_motorcycle
8. finally run this command:imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/car/01.jpg TEST_PHOTO.jpg
9. after opening vs code you should see your image with a percentage of vehicle. 

