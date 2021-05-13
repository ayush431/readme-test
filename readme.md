## Yolov4 tiny WheelChair detection -Training

## Dataset preparation 

- Downlaod the clean dataset with annotated files from [here](https://drive.google.com/drive/folders/14CME7cKxwvLd8SiPhBetGK_u8VNRsrze?usp=sharing).

## Format conversion

- Run these files `prepare_dataset/convert_json_yolo` to convert json files to yolo format (pascal format).

- To use this script your label file should be in below format.

- For example

```
filename.json

{
    "asset": {
        "format": "jpeg",
        "id": "0ac210da9f7a43c88109a6cdea97c143",
        "name": "image14.jpeg",
        "path": "file:C:/Users/vyshn/Downloads/Wheelchair%20images/image14.jpeg",
        "size": {
            "width": 275,
            "height": 183
        },
        "state": 2,
        "type": 1
    },
    "regions": [
        {
            "id": "AM-PtFHrJ",
            "type": "RECTANGLE",
            "tags": [
                "Wheelchair"
            ],
            "boundingBox": {
                "height": 171.11016949152537,
                "width": 266.84322033898303,
                "left": 3.1073446327683616,
                "top": 5.427966101694915
            },
            "points": [
                {
                    "x": 3.1073446327683616,
                    "y": 5.427966101694915
                },
                {
                    "x": 269.9505649717514,
                    "y": 5.427966101694915
                },
                {
                    "x": 269.9505649717514,
                    "y": 176.5381355932203
                },
                {
                    "x": 3.1073446327683616,
                    "y": 176.5381355932203
                }
            ]
        }
    ],
    "version": "2.2.0"
}
```
## Training

- Apart from these steps-

**step1**-In the cfg folder make a copy of the file yolov4-tiny-custom.cfg now rename the copy file to yolov4-tiny-obj.cfg.
**step2**-Change line classes=80 to your number of objects in each of 2 yolo layers.
**step3**-Change [filters=255] to filters=(classes + 5)x3 in the 2 convolutional layer immediately before each 2 yolo layers.If you have 6 classes filters=33.
**step4**-Download the pre trained weights from the link [yolov4-tiny.conv.29](https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v4_pre/yolov4-tiny.conv.29) and save it in the darknet-master folder.

all the steps are same as `darknet_yolov4_object_detection/training` directory.

**Note- You need to change name of custom cfg and pre trained weights while using training and testing command**
```
Training command-
!./darknet detector train data/obj.data cfg/yolov4-tiny-obj.cfg yolov4-tiny.conv.29 -dont_show -map
```

```
Testing command-
!./darknet detector test data/obj.data cfg/yolov4-tiny-obj.cfg backup/yolov4-tiny-obj_2000.weights -dont_show -map

```