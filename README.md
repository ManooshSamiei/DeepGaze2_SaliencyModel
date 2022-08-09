# DeepGaze2 Saliency Model
This repository contains the implementation of DeepGaze2 saliency network in Tensorflow 1.

Two notebooks are included in this repository.

## DisplayDatasets_checkpoints.ipynb

### Discription: 

- Loads two datasets SALICON and MIT1003.
- Overlays fixations on image stimuli + plot them.
- Compute center bias for both datasets + plot them.
- Compute gold standard kernel density estimate for two stimuli + plot them.
- load original checkpointed Deep gaze 2 and ICF models by authors, output their predicted densities for two arbitrary images that are not part of any of the datasets. 

### Procedure:
 
- Load pysaliency library
- Its not possible to use pysaliency like other off the shelf libraries in google colab. I clone the github reporitory of the library and modify some of its original scripts to make it compatible with google colab environment. 

- run each cell one after the other, up to the octave prompt.
- after running !octave , type below codes in the output window, inside octave prompt to run m-file in colab environment:
```
pkg load statistics
pkg update
pkg load statistics  (dont forget to load the package again after update)
run("./extract_all_fixations.m") 
```

- Wait untill all fixations are extracted, then octave command will reappear in the output cell.
You need to close the octave prompt manually by stopping the cell execution. Press on the square sign on the top left corner of the cell twice. 

- Then run the rest of the codes (upto the checkpoint predictions) to generate the plots. Here you will see two kinds of plots for each density, one using pysaliency plotting function and one using python matplotlib.pyplot library.

- Now to generate the predictions of the authors checkpointed models. first download the content of this [folder](https://drive.google.com/drive/folders/1p3z_0i8lx9whiW4elU2xePb-hvibrHYf?usp=sharing_) then upload the content of the folder in the project zip file, into the colab environment. To upload files in colab, click on the folder logo at the top left part of colab. Then click on upload sign to upload files.


## deepgaze2_Final.ipynb

### Discription: 

- Make sure to run this notebook with google colab 'gpu', otherwise the code will produce error.
- The first part of this notebook which loads the two datasets dataset is similar to the previous notebook.
- Then the pretrained weights for a normalized VGG19 network are downloaded. 
- The weights are provided as a caffe model. We should convert caffe model to tensorflow model weights to load it on our architecture. 
- The scripts for converting caffe to tensorflow are from Daan Wynen, and the reference of the code is provided at the begining of code snippets.
- Then the code for data preprocessing, building deep gaze 2 architecture, and training and testing configurations are built.


### Procedure:

- To load dataset follow the steps defined for the previous notebook.
- Then run each snippet sequentially until the end. 
- You can change the paths in the define_paths function to your desired path. 
- At the last snippet the code will ask you which phase you would like to perform? test/train. 
- Please first choose train and train the network for atleast 2 epochs.
- Then the code asks which datasets you would like to use? salicon or mit1003.
- If its the first time training, please first choose salicon.  It then automatically assigns mit1003 as its validation set, during training on salicon. 

- Then you can run the testing phase on mit1003.

**The main body structure of the code for training or testing the model, defining the arcitecture and preprocessing the data, are taken from the implementation of paper [Contextual encoder–decoder network for visual saliency prediction](https://github.com/alexanderkroner/saliency).

Please do not forget to star the repository if it was useful to your research :wink:.

I would be happy to answer any inquiries in reproducing my results.  

