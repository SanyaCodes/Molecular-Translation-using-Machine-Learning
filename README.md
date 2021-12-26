# Molecular Translation using Machine Learning

## Task :
Molecular Translation - This task can be viewed as an Image Captioning Task. Given an image of any molecule, the machine should be able to identify and process its information and generate a caption. It must be a human readable text in this case the InChI string for that molecule.

<img src="https://github.com/Ssanyachetwani/Molecular-Translation-using-Machine-Learning/blob/main/rim/task.png" alt="task" width=600/>

### File Structure :
Images of chemicals are provided, with the objective of predicting the corresponding International Chemical Identifier (InChI) text string of the image. The images provided (both in the training data as well as the test data) may be rotated to different angles, be at various resolutions, and have different noise levels.

<li> train/ - the training images, arranged in a 3-level folder structure by image_id </li> 
<li> test/ - the test images, arranged in the same folder structure as train/ </li> 
<li> train_labels.csv - ground truth InChi labels for the training images </li> 
<li> sample_submission.csv - a sample submission file in the correct format </li> 

## MY APPROACH :

### 1. Data Augmentation :
Augmentation is often used in image-based deep learning tasks to increase the amount and variance of training data. Images are flipped over x and y axis for model to adjust to various orientations.

<img src="https://github.com/Ssanyachetwani/Molecular-Translation-using-Machine-Learning/blob/main/rim/aug1.png" alt="task" width=200/>  <img src="https://github.com/Ssanyachetwani/Molecular-Translation-using-Machine-Learning/blob/main/rim/aug2.png" alt="task" width=200/>  <img src="https://github.com/Ssanyachetwani/Molecular-Translation-using-Machine-Learning/blob/main/rim/aug3.png" alt="task" width=200/>

### 2. Encoder - Decoder Architecture :
The overall structure of an encoder-decoder architecture which is commonly used is as shown below-
It consists of 3 parts: encoder, intermediate vector formed by encoder and decoder.
<li> Encoder - It accepts a single element of the input sequence at each time step, processes it, collects information for that element and propagates it forward. </li> 
<li> Intermediate vector - This is the final internal state produced from the encoder part of the model. It contains information about the entire input sequence to help the decoder make accurate predictions. </li> 
<li> Decoder - given the entire sentence, it predicts an output at each time step. </li> 

### 3. Vision Transformer as Encoder :
I will be using Vision Transformer (ViT), mostly because :
<li> Receptive field of CNNs depends on the size of their filters and the number of convolutional layers used. Increasing their value increases the complexity. ViT uses tokens instead of filters. </li>
<li> Excellent replacements for CNNs when dataset is large. </li>

### 4. Patch Encoding in ViT :
Image patches are basically the sequence tokens (like words). The PatchEncoder layer will linearly transform a patch by projecting it into a vector embedding. In short it adds a learnable attribute to the projected vector. <br/> <br/>
<img src="https://github.com/Ssanyachetwani/Molecular-Translation-using-Machine-Learning/blob/main/rim/vit.gif" alt="task" width=500/>

### 5. Transformer as Decoder :
I used Transformer, because :
<li> RNN, LSTM and GRU cannot process long sequences of data if encoded information is too long, Transformers can </li>
<li> It predicts the next word/token of the encoder output by self-attending to its own output </li>

## Evaluation 

Levenshtein distance : It is the minimum number of single-character edits required to change one word into the other
<br/>
0 or 1 : For every cell having a distance > 0, the predicted answer was termed as incorrect
<br/>
Sparse Categorical Accuracy : This metric computes the frequency with which y_pred matches y_true
<br/>
## Results :
Dataset was divided into training and testing data with 80:20 ratio. The accuracy is dependent on the Levenshtein threshold and also the correctness and neatness of the image.

| Phase | Accuracy |  
| ------- | --- | 
| Training | 84.3% |
| Testing | 76.8% |

## Demo :

<img src="https://github.com/Ssanyachetwani/Molecular-Translation-using-Machine-Learning/blob/main/rim/Demo.png" alt="task" width=600/>
