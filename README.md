# Yolo V3
You only look once (YOLO) is a state-of-the-art, real-time object detection system.
# [Part 1]
Yolo v3 on coco name Dataset

[Yolo V3 opencv-python Source](https://pysource.com/2019/06/27/yolo-object-detection-using-opencv-with-python/)

After applying the above yolo v3 model on my sample image. The output I received looks like this.
 

![Pretentious at IKEA]()

# [Part 2]

Yolo v3 on Custom Dataset.
Here, I am detecting detecting Pikachu(Pokemon character). I generated the dataset myself.
Steps for creating Dataset:
* Web crawling using python. Use [this](https://github.com/scrapy/scrapy)
* If you are lazy like me. You can use a chrome extension. [Here](https://chrome.google.com/webstore/detail/download-all-images/ifipmflagepipjokmbdecpmjbibjnakm?hl=en). There are a lot of extensions like this.
```
Note: I was too lazy for doing this. So, I didn't filter out the images. My dataset contains all type of pikachu images. Even toys, stickers and the Detective Pikachu  as well. Fortunately, it turned out to be a great model as it can detect Ryan Reynold's Pikachu as well. But don't be like me. Be smart!!
```
![Pokemon Gif]()

[Yolov3 on Custom Dataset Source](https://github.com/theschoolofai/YoloV3)

Steps are:

For custom dataset:
1. Clone this repo: https://github.com/miki998/YoloV3_Annotation_Tool
2. Follow the installation steps as mentioned in the repo. 
3. For the assignment, download 500(I used around 481) images of your unique object. 
4. Annotate the images using the Annotation tool. 
```
data
  --customdata
    --images/
      --img001.jpg
      --img002.jpg
      --...
    --labels/
      --img001.txt
      --img002.txt
      --...
    custom.data #data file
    custom.names #your class names
    custom.txt #list of name of the images you want your network to be trained on. Currently we are using same file for test/train
```
5. As you can see above you need to create **custom.data** file. For 1 class example, your file will look like this:
```
  classes=1
  train=data/customdata/custom.txt
  test=data/customdata/custom.txt 
  names=data/customdata/custom.names
```
6. As you it a poor idea to keep test and train data same, but the point of this repo is to get you up and running with YoloV3 asap. You'll probably do a mistake in writing to custom.txt file. This is how our file looks like (please note the .s and /s):
```
./data/customdata/images/img001.jpg
./data/customdata/images/img002.jpg
./data/customdata/images/img003.jpg
...
```
7. You need to add custom.names file as you can see above. For our example, we downloaded images of pikachu. Our custom.names file look like this:
```
pikachu
```
8. Pikachu above will have a class index of 0. 
9. For COCO's 80 classes, VOLOv3's output vector has 255 dimensions ( (4+1+80)*3). Now we have 1 class, so we would need to change it's architecture.
10. Copy the contents of 'yolov3-spp.cfg' file to a new file called 'yolov3-custom.cfg' file in the data/cfg folder. 
11. Search for 'filters=255' (you should get entries entries). Change 255 to 18 = (4+1+1)*3
12. Search for 'classes=80' and change all three entries to 'classes=1'
13. Since you are lazy (probably), you'll be working with very few samples. In such a case it is a good idea to change:
  * burn_in to 100
  * max_batches to 5000
  * steps to 4000,4500
14. Don't forget to perform the weight file steps mentioned in the sectio above. 
15. Run this command `python train.py --data data/customdata/custom.data --batch 10 --cache --cfg cfg/yolov3-custom.cfg --epochs 3 --nosave`

 These are the images annotated by our model 
 
 ![Image 1 ]()
 
 ![Image 2 ]()
 
 ![Image 3 ]()

[See the video output here]()