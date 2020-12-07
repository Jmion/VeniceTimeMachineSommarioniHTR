# VeniceTimeMachineSommarioniHTR

Please clone this repository using ```git clone --recurse-submodules``` to properly initalize all the submodules.

This repository is a pipeline to process the Sommarioni Venetian cadastre and to reestablish the mapping lost during the document translation.
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

### ⚙️ Step 3️⃣: Patch preprocessing
HTR preprocesseing

### 📄 Step 4️⃣: Hand writting recognition
HTR with PyLaia

### 🔮 Step 5️⃣: Establishing the link to the original document
Matching

## 🎉 Result Analysis

## License

## Contributors
Bastien Beuchat, Jeremy Mion
