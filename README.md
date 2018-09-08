# Product Classification Challenge

I used a purely computer vision approach (no use of product description) to classify each image. The output contains the top two product categories, along with their corresponding probabilites according to the classifier.

To speed up training, I used a model pretrained on ImageNet.

The solution was designed in this way to reduce the amount of training data needed. By using a pretrained model, we can avoid having to train the convolutional filters from scratch, and decent results are achieved by only adding (75 - 100) training images for each category.

I considered collecting a large training set and training a model from scratch, but this would have been fairly time consuming (both the manual training set collection as well as the model training). By using a pretrained model, I avoid training the convolutional layers and only retrain the fully connected layers at the end.

The classifier seems to be fairly confident in its shoes and jewelry predictions. My hypothesis is that these objects are fairly distinct from the others making them easier to detect. Oftentimes, it is uncertain between swimwear and intimates or skirts and dresses (this can be seen by looking at the top two classes by probability). Moreover, in certain images where the picture contains both jeans and a shirt, the model is uncertain as to whether the correct classification is 'tops' or 'jeans' which makes sense since the picture contains both. For this reason, it is useful to look at the relative probability values instead of just taking the top one. 

The solution does not cover the case where the image is unavailable. For this, we might use a word vector approach on the image description, but I have not currently implemented this. 

Additionally, I currently classify every available image, even if it does not belong to one of the given categories. If an image does not belong to any of the categories, it seems plausible that no particular category (or two) will have a very high associated probability relative to the others. By checking if this is the case, we can then mark an image as 'Others'.
