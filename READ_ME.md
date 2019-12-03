# RNA Classification

A deep learning classifier that helps to identify the different types of RNA from the provided an unafold/mfold image output. The input sequences can contain miRNA, tRNA, tRNA Pseudo, YAMAT sequences. The purpose is to identify the disease causing miRNA's precursor from the lot. 

## Getting Started

Every single cell in our body has a function. These cells has a structure, which consists of cells, nucleus and other important parts. The nucles consists of DNA, that has the instructions to build new cells. These instructions needs to be carried out of the cell to build new ones. That is done by the RNA. These RNA helps to transfer the instructions to create a new cell. There are 2 key players in RNA: mRNA and tRNA. The mRNA is the messenger RNA that consists of the messages to build the new cell. The tRNA the transfer RNA that decodes the messages from the mRNA. Thus, these help to build protein, that eventually becomes a cell, which could be hair cell, skin cell, or a nerve cell. 
    There are cases where the RNA that comes out of the nucleus doesn't really build protein. These non-coding molecules have a plenty of options to perform in our body, they can control the cell copying in bacterial cell division to inactivating the X chromosome in the nucleus. But, back in the days, they call it the "Junk DNA'. Then Victor Ambros in 1993, discovered the first non-coding gene, that was called as miRNA. Over 7 years, they didn't realize the importance, but later they started researching about. It was breakthrough in biogenesis. As of now, there are just around 17,000 miRNA sequences. Further details and explanation can be seen using the link provided under the references. 

### Prerequisites

The project is base don python 3.7. It uses the basic libraries like NumPy, Pandas, Matplotlib etc. 
In terms of sequencing, we've used the Biopython to deal witht the fasta files. Also, in order to fold the RNA, we used the ViennaRNA and forgi plot. 

You can install the the requirement.txt file by using the below command, provided you extract the clone folder

```
pip install -r requirements.txt
```

### Installing

A step by step series of examples that tell you how to get a development env running

Say what the step will be

```
Give the example
```

And repeat

```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc

