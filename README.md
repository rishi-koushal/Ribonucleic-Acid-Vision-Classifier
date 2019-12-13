# RNA Classification

A deep learning classifier that helps to identify the different types of RNA from the provided unafold/mfold image output. The input sequences can contain miRNA, tRNA, tRNA Pseudo, YAMAT sequences. The purpose is to identify the regulatory molecule miRNA's precursor from the lot. 

## Why? and How?

Every single cell in our body has a function. These cells have a structure, which consists of mitochondria, Plasma membrane nucleus and other such important parts. The nucleus consists of DNA, that has the instructions to build new cells. These instructions needs to be carried out of the cell to build new ones. That is done by the RNA. These RNA helps to transfer the instructions to create a new cell. Two important RNA molecules are: mRNA and tRNA. The mRNA is the messenger RNA that consists of the messages to build the new cell. The tRNA the transfer RNA that decodes the messages from the mRNA. Thus, these two help to build protein, that eventually becomes a cell, which could be  a hair cell, skin cell, or a nerve cell. 

There are cases where the RNA that comes out of the nucleus doesn't really translate to protein. These are called non-coding molecules, which eventually have plenty of options to perform in our body. They can go from controlling the cell copying in bacterial cell division to inactivating the X chromosome in the nucleus. But, back in the days, they call it the "Junk DNA'. But, Victor Ambros in 1993, discovered the first non-coding gene, that was called as miRNA. They didn't the amount of danger these small molecules could lead to. There are several research that takes places even now on these miRNAs. A strong association has been found between dysregulated miRNA molecules and various diseases such as cancer, neuro disorders, and autoimmune diseases. They play a crucial role in one of the most important cellular functions known as gene expression.

We have built a vision classifier which will identify miRNA molecules based on their secondary structures. The secondary structure of a miRNA generally resembles a hairpin while the secondary structure of a tRNA generally resembles a clover. The main issue however is that there are tens of variations of tRNA and thousands of miRNA variations and even more non-tRNA and non-miRNA types of RNA. The classifier then must distinguish between miRNA, tRNA and other RNA molecules that may even resemble miRNA or tRNA.

### Prerequisites

The project is based on python 3.7. It uses the basic libraries like NumPy, Pandas, Matplotlib, etc. 
In terms of sequencing, we've used the **Biopython** to deal with the fasta files. Also, in order to fold the RNA, we used the **ViennaRNA's forgi plot**

You can install the the requirement.txt file by using the below command, provided you extract the clone folder

```
pip install -r requirements.txt
```

If you'd like to jump directly, please look into to Part_1 notebook and then Part_2 notebook. Brief description is given in the notebooks as well. 

### Workflow

As soon as you install the requirements.txt, please make sure you've installed [ViennaRNA](https://github.com/ViennaRNA/ViennaRNA) locally. You can check your local installation by running the code ``` import RNA```. The process can be briefly classified into 5 steps:

##### 1. Reading the fasta file

Most of the RNA sequences will be infa (fasta format). This file consists of list of RNA sequences and their IDs, description etc. Our job in this step is to make use of Bio python's powerful feature to extract the sequences and their ID's for homo sapiens alone. The below code snippet will let us understand the procedure


```
for seq_record in SeqIO.parse(open(file_in, mode='r'), 'fasta'):
        seq_record.description=' '.join(seq_record.description.split()[1:])   
        seq_id.append(seq_record.id)
        seq.append(seq_record.seq)
        desc.append(seq_record.description)
```

Following this step, we can do some preprocessing to the sequences like joining the letters without the commas etc.

##### 2. Plot the Secondary Structure

The RNA secondary structure plays an important role in this project. We're using ViennaRNA's forgi plot to obtain the secondary structure. Make sure you install the dependencies before you execute the notebook code. The code snippet will look like

```
cg = forgi.load_rna("examples/input/tRNA/0.fx", allow_many=False)
a = fvm.plot_rna(cg, text_kwargs={"fontweight":"black"}, lighten=0.5,
             backbone_kwargs={"linewidth":1})

```

![RNA](/media/mit.png)


##### 3. Creating the Dataset

Here, we not only focus majorly on miRNA, but also the tRNA that actually help to build the protein. The typical function of the tRNA is to decode the mRNA's instructions. Inorder to classify them, we must manually label them in order to create the perfect dataset for our model. The generic shape of miRNA will be hairpin and tRNA will be a clover leaf. With the help of multi label pigeon, we can annotate them really quick

```
annotations = annotate(images,
    options=['tRNA','miRNA','Neither'],
    display_fn=lambda filename: display(Image(filename))
    )

```

Thus, we end up creating a dataset with image name with their corresponding label (miRNA, tRNA, neither). You can download the dataset from [link](https://drive.google.com/open?id=1g807ROiCf1w1Mn8cFpMRnzoknVB4jDuL)

##### 4. Building the Vision Classifier Model

Now, we've come to the step where we build a classifier. We're using fastai's vision classifier. The initial step is to build a data bunch with normalized images. **Since the RNAfold images are on the same dimensions we don't really require the data augmentation step, but it is always good to perform the data augmentation when we're working with images**. Following this step, we build a classifier using the pre trained resnet34 model. (Thanks to fastai!) 

```
cnn_learner(data, models.resnet34, metrics=accuracy)
```

Now we can train the model with the data bunch by finding the appropriate learning rate.

##### 5. Observing the model performance

Since it is a classifier, we can use fastai's classification interpreter to plot a confusion matrix. We can use the code snippet to plot them.

```
interp.plot_confusion_matrix(figsize=(6,6))
```

Now we can train the model with the data bunch by finding the appropriate learning rate.


### Our Progress and Performance results

We built the dataset with 900+ images. Also, our model was trained using resnet34, resnet50 and densenet121. We were able to obtain fairly considerable accuracy of 94%. 


### Points we'd like to raise

We tried to build the dataset from the fasta files available from 
* [miRBase](http://mirbase.org)
* [gtRNAdb](http://gtrnadb.ucsc.edu)

There's a claim that says that there are some false positives in the tRNA sequences. This would play a role in the model. There's a scarcity in high confidence tRNAs. It would be great if we could build the dataset furthermore and try to classify other role playing molecules like siRNA. 

## References

We'd like to thank all the open source libraries, forums that helped us in this project. 

* [BioStars](https://www.biostars.org/)
* [Forgi Plot](https://viennarna.github.io/forgi/graph_tutorial.html)
* [RNAfold](http://rna.tbi.univie.ac.at/cgi-bin/RNAWebSuite/RNAfold.cgi)
* [Multilabel Pigeon](https://github.com/tzutalin/labelImg)
* [ViennaRNA](https://github.com/ViennaRNA/ViennaRNA)
* [ResearchPaper](https://ieeexplore.ieee.org/document/6999274)
* [ResearchPaper](https://www.nature.com/articles/srep25941)
* [ResearchPaper](https://arxiv.org/pdf/1610.02281.pdf)
* [ResearchPaper](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=5565611)
* [Fastai](https://www.fast.ai)

and other blogs, tutorials.


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

We'd like to thank [Phillipe Loher](https://cm.jefferson.edu/staff-members/phillipe-loher/), Director of Machine Learning, [Thomas Jefferson University](https://cm.jefferson.edu/) and Professor Stephen Welch for mentoring and guiding us throughout this project.

We're happy to receive any suggestions and ideas you'd like to improve this project.
 
