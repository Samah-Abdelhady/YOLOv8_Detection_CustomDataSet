# YOLOv8

In this repo, you learn how to use YOLOv8 in object detection task, in your local machine "linux" with custom dataset.

It is better to create a virtual environment first, then work with YOLOv8 inside. To Create avirtual machine, do the following:
1. Open the terminal ```ctrl+alt+t```
2. Install "python3-venv" package, if it is not installed: ```sudo apt install python3-venv```
3. Create the virtuak environment: ```python3 -m venv venv-name```
4. Activate the virtual environment: ```source venv-name/bin/activate```
5. Move your terminal inside the virtual environment: ```cd venv-name```


### 1. Detection task

1. Install all the reuired modules for YOLOv8: ```pip install ultralytics```
2. Prepare the custom data set
	* Create a folder for the dataset "ex: data".
	* Inside "data" folder, create "data.yaml" file.
	* Inside "data" folder, create 3 folders "train, val, test".
	* In each folder "train, val, test", create "images, labels" folders.
	* Set the test, train, and validation data inside their folders.
	* Open "data.yaml" file, and set the data path:
		```
		  train: data/train/images
		  val: data/train/images
		  nc: 2
		  names: ['cat', 'dog']
		```
3. Train the model:
	* From python script:
	 ```
       from ultralytics import YOLO
	   #model = YOLO()#train the model from scratch
	   model = YOLO("yolov8n.pt")#train based on pre-trained model
	   model.train(data="data.yaml", epochs=100)
	 ```
	* From terminal:
	 ```
	    yolo task=detect mode=train model=yolov8n.pt data=data.yaml epochs=100 imgsz=640
	 ```
4. Validate the model:
	* From python script:
	 ```
       from ultralytics import YOLO
	   model = YOLO("best_model_weights_path.pt")
	   model.val(data="data.yaml")
	 ```
	* From terminal:
	 ```
	    yolo task=detect mode=val model="model_path/best.pt" data=data.yaml
	 ```

5. Test the model:
	* From python script:
	 ```
	   from ultralytics import YOLO
	   model = YOLO("yolov8n.pt")
	   model.predict(source="image.png")
	 ```
	* From terminal:
	 ```
	   yolo task=detect mode=predict model=best_model_path.pt conf=0.50 source=test_images_folder/OR/"image.png"
	 ```

