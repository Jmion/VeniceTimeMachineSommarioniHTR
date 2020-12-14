# VeniceTimeMachineSommarioniHTR

Please clone this repository using ```git clone --recurse-submodules``` to properly initalize all the submodules.

This repository is a pipeline to process the Sommarioni Venetian cadastre and to reestablish the mapping lost during the document translation.
This pipeline was established during course  Foundation of Digital Humanities (DH-405) given in fall 2020 at EPFL.
To have more context and explanation about the project please refer to the project [wiki page](http://fdh.epfl.ch/index.php/Deciphering_Venetian_handwriting).
Please find the details on how to run the pipeline below:

## Historical context
The Sommarioni cadastre priginates from the efforts done by the Venice Time Machine project to archive and digitilize parts of the venetian archives.
During this process the land registries called cadastres where scanned to produce high quality images. These documents were then translated by humans
to produce a spreadsheet containing a digital version of the cadastre. Sadly the link to the origininal page of the cadastre was lost during this process,
this is where our project comes into play. This pipeline allows us to reestablish this lost link using high quality scans of the original documents. As an example please find bellow an image on a page from the cadastre:

<img src="http://fdh.epfl.ch/images/2/29/Censo-stabile_Sommarioni-napoleonici_reg-1_0015_013.jpg" width=40% class="center">

## 🏃 Pipeline
### 📝 Step 1️⃣: Baseline detection
The first step of the pipeline concists in using the P2PaLA to extract the baselines from the images of the cadastre. For more details on how to use P2PaLA please look at the README in P2PaLA to understand how to use this. Use the [egs directory](https://github.com/lquirosd/P2PaLA/tree/1cb2b7658b54db1e37324ee9b24fc333acb65779/egs/pre_trained) showing how to use the project with a pre-trained model. This model works well on the Sommarioni cadastre.

![line detection](https://github.com/Jmion/VeniceTimeMachineSommarioniHTR/blob/master/Line_detection.png)

### 📜 Step 2️⃣: Patch extraction
After running the P2PaLA the page layout will have been exported in a [PAGE](http://www.primaresearch.org/tools/PAGELibraries) layout description, the xsd schema of the document produced can be found [here](https://www.primaresearch.org/schema/PAGE/gts/pagecontent/2019-07-15/pagecontent.xsd).
The PageExtractor submodule will allow you to extract the patches containing text from the full page scans. Please refer to the README in that submodule to understand how to use it. This is an important step since the HTR model takes as an input a single word or sentence and cannot process the entire page.

### 📄 Step  3️⃣: Hand writting recognition
This part of the pipeline is done with [PyLaia](https://github.com/basbeu/PyLaia). To setup the PyLaia framework the [IAM example](https://github.com/basbeu/PyLaia/tree/master/egs/iam-htr) provide the steps that are required.

Running this step on Patch extracted will require some pre-processing. The exact instructions to reproduce the run of the project is given in the [PyLaia repository](https://github.com/basbeu/PyLaia#fdh-project---decipher-venice).
The training step is not needed as a trained model is provided in the repository.

### 🔮 Step 4️⃣: Establishing the link to the original document
The goal here is to wrap the previous step together in order to deliver the final output. The final mapping map a line in the excel file to a digitized page of Sommarioni. This step also provide IIIF link to the matching. The IIIF links are in this form : [https://images.center/iiif_sommarioni/reg1-0003/0,2578,6000,132/full/0/default.jpg](https://images.center/iiif_sommarioni/reg1-0003/0,2578,6000,132/full/0/default.jpg).

The implementation of this step can be found in the dedicated repository [MatchingSommarioni](https://github.com/basbeu/MatchingSommarioni)
The code of the matching is provided in two jupyter notebooks. The main notebook is Matching.ipynb. Given the input computed in step 2 and 3 of the pipeline and the main excel file, it outputs the results.csv file.

The second notebook called Patch_statistics.ipynb is a short exploratory data analysis to show the reasons behind the design choices of the data wrangling step implemented in the main notebook.

## 🎉 Results
The accuracy on the test set is 0.578. 
It means that the pipeline make sense but that it can be improved. The results are not very impressive because we think that the system with such an accuracy is not very usable. Nevertheless, it could be handy to find some patches/lines via the IIF links and at least the output is very interpretable. 
If a user reading the transcribed file wants to go back to the source, we think that it is very fast via the IIIF links to see the matching. In the case of a matching success, the user will save a lot of manual searching time. In case of failure, the user will not lose too much time as we think that he will realize very quickly that the matching is not correct.

## License

## Contributors
Bastien Beuchat, Jeremy Mion
