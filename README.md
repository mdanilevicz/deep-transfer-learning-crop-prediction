# Deep  Transfer  Learning  for  Crop  Yield  Prediction  with  Remote Sensing  Data

This project implements the deep learning architectures from [You et al. 2017](http://sustain.stanford.edu/crop-yield-analysis/) and applies them to developing countries with significant agricultural productivity (Argentina, Brazil, India).

We also examine the efficacy of transfer learning of yield forecasting insights between adjoining countries; some results were published in the proceedings of [COMPASS 2018](https://acmcompass.org/program/). Our paper can be viewed [here](https://www.dropbox.com/s/ei49eck573yxi6f/deep-transfer-learning.pdf?dl=0).

Contributers:
[Anna X Wang](annaxw@cs.stanford.edu), [Caelin Tran](caelin@cs.stanford.edu), [Nikhil Desai](nikhild@cs.stanford.edu), Professor David Lobell, Professor Stefano Ermon

# Instructions for creating a dataset
Steps marked with (`#`) should be done if the country of interest is not the US, India, Brazil, or Argentina
1. (`#`) Edit `pull_modis.py` to specify shapefile source, and how to extract relevant metadata (human-readable name, criteria for pulling imagery) from shapefiles (TODO: add more detail)
1. Run `pull_modis.py` with country and imagery type to download imagery to a Google Cloud bucket
2. Put satellite imagery into "sat" folder, temperature images into "temp" folder, cover images into "cover" folder
3. Run `histograms.py` with the sat,temp,cover folders specified arguments - outputs to a "histograms" folder
4. (`#`) Save a CSV containing yields for relevant set of regions, harvest years, and crop types. (TODO: more explanation of the yields CSV format)
4. Run `make_datasets.py` with the "histograms" folder and yields CSV, along with relevant parameters for use in ML (train/test split, years to ignore or to use, etc) - creates a "dataset" folder containing numpy arrays which will be used by training/testing architecture

# Instructions for training the model
1. Run `train_NN.py` with a dataset name and neural net architecture type (CNN or LSTM). Generates a "log" folder containing the model weights, model predictions, and logs tracking model error.
2. Look inside the log folder for model results.

# Instructions for fine-tuning a trained model on a different dataset
1. Run `train_NN.py` on a dataset folder "X" as above. Generates a "log" folder.
1. Run `test_NN.py` and pass in as arguments the "log" folder from training, along with a new dataset folder "Y" on which to fine-tune the model.
2. Result is a new folder "log2" containing the new model weights, predictions, and error logs for performance on dataset "Y".
