# ReLayNet

Code and Trained Models

-----------------
If you use this code, please cite:

A. Guha Roy, S. Conjeti, S.P.K. Karri, D. Sheet, A. Katouzian, C. Wachinger, and N. Navab, 
"ReLayNet: retinal layer and fluid segmentation of macular optical coherence tomography using fully convolutional networks," 
Biomed. Opt. Express 8, 3627-3642 (2017) 

If you face any issues running the code, let me know by posting in issues.

Enjoy!!! :) 

PyTorch Implementation of this code available at: https://github.com/abhi4ssj/relaynet_pytorch

------------------


# Usage: 

1. Download MatConvNet and Compile it (Follow: http://www.vlfeat.org/matconvnet/install/)

2. Unzip ReLayNet folder. Copy files:

Copy /layers/matlab files/ ---> <MatConvNet_HomeFolder>/matlab/

Copy /layers/dagnn wrappers/ ---> <MatConvNet_HomeFolder>/matlab/+dagnn/

3. Copy Rest of the files in another home Folder

4. Create an experiment Folder ex: 'Exp01_ReLayNet_LayerAndFluidSegmentation'

5. Create Imdb of the dataset (Follow instructions below)

It is basically a structure: 

imdb.images.data is a 4D matrix of size: [height, width, channel, NumberOfData]

imdb.images.labels is a 4D matrix of size: [height, width, 2, NumberOfData] ---> 1st Channel is class (1,2,... etc), 2nd channel is Instance Weights (All voxels with a class label is assigned a weight, details in paper) 

imdb.images.set is [1,NumberOfData] vector with entries 1 or 3 indicating which data is for training and validation respectively.

6. RunTraining: 

[net, info] = ReLayNet(imdb, inpt); 

where initialize, inpt.expDir = 'Exp01_ReLayNet_ChoroidSegmentation'

7. In the code check the hyper parameters like learning rate, number of class, epochs etc

-----------------------------

# Deployment of Model

The folder Trained Model consist of 8 Models from 8 Fold Cross Validation from the paper

In the RunFile folder, the function 'EnsembleTest' takes in a OCT scan from a specified Directory and File Extension. Provides the 10 Class segmentation as an average of predictions from all 8 models.

The performance was tested with decent results from Heidelberg Engineering (Spectralis) OCT Machine. 

For other OCT scans (eg: Nidek, Cirrus) dedicated models need to be trained.

The classes corresponding to segmentation IDs are:

[Cls 1:] Region above the retina (RaR); 

[Cls 2:] ILM: Inner limiting membrane;  

[Cls 3:] NFL-IPL: Nerve fiber ending to Inner plexiform layer; 

[Cls 4:] INL: Inner Nuclear layer; 

[Cls 5:] OPL: Outer plexiform layer; 

[Cls 6:] ONL-ISM: Outer Nuclear layer to Inner segment myeloid; 

[Cls 7:] ISE: Inner segment ellipsoid;

[Cls 8:] OS-RPE: Outer segment to Retinal pigment epithelium; 

[Cls 9:] Region below RPE (RbR)

[Cls 10:] Fluid region

-----------------------------

