# VeniceTimeMachineSommarioniHTR

Please clone this repository using ```git clone --recurse-submodules``` to properly initalize all the submodules.

This repository is a pipeline to process the Sommarioni Venetian cadastre and to reestablish the mapping lost during the document translation.
Please find the details on how to run the pipeline below:

## 🏃 Pipeline
### Step 1: Baseline detection
The first step of the pipeline concists in using the P2PaLA to extract the baselines from the images of the cadastre. For more details on how to use P2PaLA please look at the README in P2PaLA to understand how to use this. Use the [egs directory](https://github.com/lquirosd/P2PaLA/tree/1cb2b7658b54db1e37324ee9b24fc333acb65779/egs/pre_trained) showing how to use the project with a pre-trained model. This model works well on the Sommarioni cadastre.

### Step 2: Patch extraction
After running the P2PaLA the page layout will have been exported in a [PAGE](http://www.primaresearch.org/tools/PAGELibraries) layout description, the xsd schema of the document produced can be found [here](https://www.primaresearch.org/schema/PAGE/gts/pagecontent/2019-07-15/pagecontent.xsd).
The PageExtractor submodule will allow you to extract the patches containing text from the full page scans. Please refer to the README in that submodule to understand how to use it.

### Step 3: Patch preprocessing
HTR preprocesseing

### Step 4: Hand writting recognition
HTR with PyLaia

### Step 5: Establishing the link to the original document
Matching
