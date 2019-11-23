## Intrinsic dimension of data representations in deep neural networks



This is the repository associated to our **NeurIPS 2019** paper

["Intrinsic dimension of data representations in deep neural networks"](https://arxiv.org/abs/1905.12784)

**Paper Authors**

Alessio Ansuini (1),  Alessandro Laio (1),  Jakob H. Macke (2),  Davide Zoccolan (1)

(1) International School for Advanced Studies (SISSA)  https://www.sissa.it/ 

(2) Technical University of Munich (TUM)  https://www.tum.de/



*Alessio Ansuini wrote the following contents: he is the only one to blame for any error in these github pages.*





<img src="./docs/figs/wrap_up.png" width="600" />



### Contents

We provide

- a **brief outline** of our work
- a few [**tutorials**](https://github.com/ansuini/IntrinsicDimDeep/tree/master/tutorials) where we also point to possible extensions and open problems
- detailed instructions for **reproducibility** of our results
- **extra materials** (videos, slides, etc.)

### Extras

- to frame this research in a broader perspective - embracing Neuroscience and Deep Learning - we point to the **seminar** given by Davide Zoccolan at the [ICTP Workshop on Science of Data Science | (smr 3283)](https://www.youtube.com/watch?v=nO13-AHit6E)

### Outline of our work

Datasets can be very high-dimensional. It is very common, for example, that images from experiments (nanotechnology, biology, astrophysics etc.),  and from ordinary life, have 1M pixels, each one counting for a dimension in the data space.

Of course, there is rich structure in interesting datasets, and this induces correlations and (soft) constraints among the dimensions, that reflect geometrically on the fact that data lie in the neighbourhoods of low-dimensional manifolds. We call *embedding dimension* (ED) the dimensionality of the space hosting the data and *intrinsic dimension* (ID) the dimensionality of the manifold that approximates the data points. 

In our work we study the ID of data representations in the hidden layers of deep neural networks (DNN). It is well known that DNNs - in particular convolutional networks (CNN) - transform their input from the original space (pixels, sounds, etc.) to a progressively abstract form, that support classification and, eventually, downstream actions.  

We follow the evolution of representations along the layers of CNNs focusing on its intrinsic dimension, using the method of estimation described in a recent paper by one of us: [Estimating the intrinsic dimension of datasets by a minimal neighborhood information]( https://www.nature.com/articles/s41598-017-11873-y).

The idea of studying the intrinsic dimension of representations in deep network is not new. Many works already addressed this problem, with different approaches, and we refer to our paper for a  brief (due to lack of space) discussion of these works. 

**Main findings**

Our main findings are:

- the ID profile, across a relevant number of state-of-the-art (pretrained) CNNs follows a curved shape that we informally nicknamed the "hunchback"

  (to compare many different architectures we plotted the ID vs. a relative depth, which is the number of non-trivial transformations that the network performs on the input (convolutional and fully-connected layers' operations) divided by the total number of these transformations before the output)

  

<img src="./docs/figs/hunchbacks_cb_panel_B.png" width="700" />



- the ID in the last hidden layer (for the same set of networks) is predictive of its generalization performance

  (this result holds across and within architecture classes, see for example the inset for ResNets)

  

<img src="./docs/figs/lasthidden_cb.png" width="700" />



- representations in hidden layers lie typically on *curved manifolds*.

  This result may not be surprising for the input and intermediate layers: it is commonly accepted that, due to the complex constraints that shape categories, object manifolds are typically twisted and curved.

  But we observed that also representations in the last hidden layer are curved, and this indicates that a flattening of data manifolds may not be a general computational goal that deep networks strive to achieve: progressive reduction of the ID, rather than gradual flattening, seems to be the key to achieving linearly separable representations.  

  A linear approach to dimensionality estimation based on PCA was unable to capture the actual dimensionality of representations. For example, we did not found clear eigenvalues gaps in the correlation matrix (normalized or not) and this is for itself an indication of curvature (but more evidence is provided in the paper, see for example Fig. 5 panel B)

  A linear estimate based on PCA that we looked at is the number of eigenvectors that capture the 90 %​ of variance in the data; we called this dimensionality estimate PC-ID.

  What we found is that this PCA-based measure gives much higher values of the ID and is not able to distinguish qualitatively between trained and untrained networks. On the contrary, our ID estimate shows that for untrained networks the ID is substantially flat.

  We observe that this is consistent with the fact that random linear transformations (neglecting the effect of non-linear activation functions) in high-dimensional space are close to orthogonal and thus it will tend to leave the intrinsic dimension of a low-dimensional manifolds, embedded in the source space, unchanged.

  

  

  
  
  <img src="./docs/figs/curvature_cb_panel_C.png" width="700" />



**Further results**

We performed further experiments on the dynamics of the ID. These line of research is very important, in particular for the development of unsupervised approaches, as is stated in some precedent works we referred to in our paper.

But from the evidence we collected and from the results we found in the literature we are not able to draw definitive conclusions yet.

We performed these experiments on a VGG-16 network trained on CIFAR-10; the architecture and the optimization procedure used for these experiments is taken from https://github.com/kuangliu/pytorch-cifar.

Our main observations are:

- during training different layers show different dynamics.

  This is already clear from the figure above, by comparing the ID of untrained and trained VGG-16 (respectively, black dashed and continuous line). 

  In new experiments, described in the Supplementary Materials, we also found that 1) the final layers compress representations 2) the initial and intermediate layers expand it.

  In the following figure, we can easily appreciate these findings by looking at how the ID in the untrained network (thick black line), gradually transforms into the ID profile of the fully trained network (light yellow).
  
  

<img src="./docs/figs/suppl_dynamics_cb_panel_A.png" width="700" />

​    

Taking a closer look to the early phases of training (now focusing only on the last hidden layer) we also found that, after a first compression phase (lasting approximately a half-epoch) the ID slowly expands and stabilizes to a higher value. This *change of regime* (from compression to expansion) is not accompanied in this case to the onset of overfitting, as it was observed in other works that used *local* measures of intrinsic dimension. It is important, for such comparisons, to remember that our ID estimate is a *global* one. 

Overall, we think that the dynamics of the ID is not well understood, perhaps depending strongly on the architectures, datasets and optimization procedures (including small details such as learning rate, batch size etc.), and a sound understanding of how all these factors can have an influence on it requires further investigations.





<img src="./docs/figs/suppl_dynamics_cb_panel_C.png" width="700" />

### Tutorials (work in progress)

We provide the following tutorials:

- Extraction and ID computation on a small convolutional network (MNIST)
- Multi-scale analysis (block-analysis)

- Extraction and ID computation in a VGG-16 (ImageNet)
- Dynamics of the ID in VGG-16 (CIFAR-10) 

### Reproduction of results

**Main dependencies**

- Python (3.6.7)
- Pytorch 1.0 (torch 1.0.1.post2, torchvision 0.2.2)
- numpy (1.16.2)
- scikit.learn (0.20.3)
- tqdm (4.31.1)
- torchsummary

We will refer as ROOT as the root of the repository directory: IntrinsicDimDeep.  

**Results in main text**

We will discuss how to reproduce the main results in order of appearance in the main text.

First of all you will have to download and unzip in the ROOT the data provided at this [link](https://figshare.com/s/8a039f58c7b84a215b6d).

- **Figure 2: VGG-16-R on a custom dataset**

  You can plot the results of a typical run just by opening the notebook plots.ipynb in scripts/custom. 

  If you want to do the  training and analyze your results you can do as follows:

  - change directory into data/custom

  - generate the train/test split:
  
    ```
  ​```
    $python train_test_split.py
  ​```
    ```

    
  
  - change directory to scripts/custom 

  - launch finetuning:

    ```
  $ python finetune
    ```
  
    This will finetune a VGG-16 pre-trained on ImageNet. At the end it will also extract representations and save them in data/custom/results by default

  - run the bash script
  
    ```
    $ ./run.sh
  ```
  
    This will analyze the extracted representations and generate the data (sav-
  ing it by default) required for Figure 2 (there can be small fluctuations
    due to the number of epochs of training that you use and/or the random
    splitting between train and test).
  
    
    
  You can visualize your results opening the notebook plots.ipynb in scripts/custom,
    decommenting the line that specifies to use your results.
    
    This pattern of usage will be maintained for all the experiments below.



- **Figure 3 (generality of the "hunchback" shape)**

  To show the results of a typical run

  - change directory to scripts/pretrained
  - open and run the notebook hunchback.ipynb

  To re-create the data from scratch:

  - ```
    $ ./last_hunchback.sh
    ```

    

- **Figure 4 (ID and generalization)**

  To show the results of a typical run

  - change directory to scripts/pretrained
  - open and run the last_hidden.ipynb

  To re-create the data from scratch:

  - ```
    $ ./last_hidden.sh
    ```



- **Figure 5 (Curvature)**

  To show the results of a typical run

  - change directory to scripts/pretrained
  - open and run the last_hidden_pca.ipynb

  To re-create the data from scratch:

  - ```
    $ ./last_hidden_pca.sh
    ```

  

- **Figure 6 (MNIST)**

  To show the results of a typical run

  - change directory to scripts/mnist
  - open and run the plot.ipybn

  To re-create the data the procedure is slightly longer than in the preceding cases:

  - train the small convolutional network on all the datasets (MNIST,MNIST* and MNIST+)

    ```
    $ ./train_all.sh
    ```

    You could do the three trainings separately:

    ```
    $ ./mnist.sh
    ```

    ```
    $ ./mnist_grad.sh
    ```

    ```
    $ ./mnist_shuffled.sh
    ```

  - analyze the results in the three cases:

    ```
    $ ./analyze_all.sh
    ```

    

    The epochs specified as parameters in analize_all.sh are by default the same used to train the different models.

    Anyway, for exploration purposes you can choose at which epoch to extract the data.

    ```
    $ python analyze.py --dataset yourdataset --epoch yourepoch
    ```

  -  The shuffled dataset (MNIST+) and the dataset perturbed with the luminosity gradient (MNIST*) are provided. Anyway, you can create a new shuffled dataset

    ```
    $ python create_shuffled_mnist.py --save 1
    ```

    and / or a new MNIST perturbed with a higher or lower stretching parameter lambda

    ```
    $ python create_mnist_with_gradient.py --save 1 --lambdavar yourlambda
    ```

    

  

















