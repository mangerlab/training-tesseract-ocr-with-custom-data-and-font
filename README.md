# Training Tesseract-OCR with Custom Data and Font

# Important

* These instructions do not support LSTM models, it is better to stack pre-trained models as I discovered later *

Based on https://medium.com/@riasharma.indian/training-tesseract-ocr-with-custom-data-and-font-cf9e94429b4a by Ria.

## Requirements

* [Tesseract](https://github.com/tesseract-ocr/tesseract)
* [Java](https://www.java.com/en/download/)
* [jTessBoxEditor](https://github.com/nguyenq/jTessBoxEditor)
* Images in PNG or TIFF format. You can batch convert images to PNG or TIFF using ImageMagick. The advantage of TIFF is that it can store multiple pages in a single file.

## Run jTeassBoxEditor

Run the following commands in the terminal:

```bash
wget https://github.com/nguyenq/jTessBoxEditor/releases/download/Release-2.6.0/jTessBoxEditor-2.6.0.zip
unzip jTessBoxEditor-2.6.0.zip
cd jTessBoxEditor
java -Xms128m -Xmx1024m -jar jTessBoxEditor.jar
java -Dswing.defaultlaf=javax.swing.plaf.nimbus.NimbusLookAndFeel -Xms128m -Xmx1024m -jar jTessBoxEditor.jar
```

### On TIFF/Box Generator

1. Create transcribe one of your images in a txt file and open it in the input box (`megaman-example/start.png` and `megaman-example/start.txt` in this repo).
2. Select the output folder (`megaman-example` in this repo).
3. Select the font and size (being this an "exotic" example, I downloaded the Mega Man X font from [here](https://fontstruct.com/fontstructions/show/1038596/mega_man_x_1) and set it to 12pt after looking at the image).
4. Give a name to your model.
5. Select generate. This will create a TIFF file from the PNG image.

### On Box Editor

1. Open the TIFF image created in the previous step.
2. Tesseract generates box files for the text in the images. Tesseract will try draw boxes around the characters and to identify them. This is not 100% accurate, otherwise there is no need to train Tesseract.
3. Click on each of the boxes and check that in Box View the correct character is displayed.
4. Click on any missed characters and indicate with letter/number they should be.
5. Click on Save.

## On Trainer

1. Check the data path, language and model. Select Train With Existing Box model and use the box file created in the previous step.
2. Click on Run and then Validate on the original image. The result shows this (expected because we are training with a single image with little text): `& GAME START PASS WDRD DPTLON MDDE`.
3. The trained data will be saved in `tessdata/eng.traineddata` (or the language you selected).

## Copyright

Megaman X is a trademark of Capcom. The font used in this example is a fan-made font by Patrick H. Lauke and it is released under the Creative Commons license.
