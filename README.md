# chexnet_auroc
This is a chexnet implementation on a custom dataset with auroc calculations.

AUROC is an important statistic that tells us if a model is able to successfully disinguish between positive and negative examples.
I used the Kaggle RSNA Pneumonia challenge dataset and converted the dicom files to jpg. Then I split the stage 1 training data into a
training and validation set. I used the stage 1 test set as the test set.

The architecture mostly follows the chexnet architecture with a couple of extra features thrown in. I used a great data generator from 
https://github.com/brucechou1983/CheXNet-Keras that implements both threaded data generation and augmentation. I added in model warmup
that enables faster convergence. I also tweaked the class activation map code to make it work for my case.

Below are the results. Everything on the left of the vertical red line is a correct estimate of presence or absence of pneumonia.
On the right of that line are wrong guesses i.e the model predicted pneumonia where none existed and vice versa.

![1](https://github.com/varunvprabhu/chexnet_auroc/blob/master/output/blog_combo_output.png)

In the correct predictions in the image, the top row is the one that the model predicted the presence of pneumonia. 
The blue rectangles are radiologist estimates of where pneumonia is present in the lungs and the multicolored areas are the model 
predictions for the same. We can see that in the correct predictions they overlap indicating the model is able to 'see' pneumonia in the 
same way as a radiologist.

In the bottom row of correct predictions, we can see that the model excludes the lungs areas, which is the same as saying that it is 
unable to find pneumonia like features in those areas.

For incorrect predictions, in images where there's not much activation, it's supposed to predict Pneumonia but it predicts 'Normal' 
meaning those are False Negatives. In the brightly colored images, it's the opposite, meaning those are False Positives.

Code uses: Keras with Tensorflow backend. Jupyter notebook for code compilation.
