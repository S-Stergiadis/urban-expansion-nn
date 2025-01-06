# Overview
This script was part of research funded by and conducted for the Dragon 5 ESA (European Space Agency) initiative. It processes satellite imagery data, preparing it for training a ConvLSTM model to predict urban expansion. The data is augmented and preprocessed to improve model performance and reduce overfitting. Its more of an explorative analysis rather than a robust deployable predictive model, trying to assess how far someone can get assuming the system does not depend on any exogenous variables using a non-Markovian model. 

# Files
 - uexp.ipynb contains the code
 - combined_urban_expansion_*.tif contains urban expansion data from 1985 till 2018 obtained from the [Tsinghua FROM-GLC GAIA v10](https://developers.google.com/earth-engine/datasets/catalog/Tsinghua_FROM-GLC_GAIA_v10) dataset. Each raster corresponds to a single year.
 - the pdf is the associated poster paper for the 2024 Dragon symposium that took place in Lisbon from 24/06/2024 - 28/06/2024
 - The h5 file is the trained model
 - dl_environment.yml contains all the dependancies of the environment used to run the script
 - model.h5.png is visual representation of the model

# Potential Improvements
Due to technical limitations (you can only train a so-large model on a decent laptop 🙂), the model trained had fairly few parameters. If this poses no limitations to you, the following options/improvements might be worth exploring:

## Data
- Use more of or the entire dataset, [Tsinghua FROM-GLC GAIA v10](https://developers.google.com/earth-engine/datasets/catalog/Tsinghua_FROM-GLC_GAIA_v10), to ensure the model generalizes correctly and therefore makes more accurate predictions.
- Include exogenous variables with good candidates being socio-economic statistics like:
  - Population density
  - Income
  - Crime
  - Housing prices
  - Infrastructure (commuting, schools, hospitals)
- Find a better solution/loss function for the class imbalance problem.

## Model Architecture
- The thresholding applied to the predictions could probably be incorporated into the model's architecture.
- More complex models (e.g., more layers, more kernels, or both) could perform better.
- While ConvLSTMs are good at capturing spatio-temporal patterns, there are newer models that can be tested if computational resources are available. GAN's are good candidates that could also deal with the class imbalance as they learn the distribution of the data. Since the input data are images diffusion models could also be effective given their performance with image generation.

## Training
- Include cross-validation if the dataset remains small.
- Fine-tune the model with hyperparameter optimization. Parameters that would be interesting to investigate include:
  - Input sequence length
  - Kernel size

## Approach

- Instead of going for a "predict-the-next-frame" approach, a direct prediction would be better since the system's dynamics have a large timescale.
- Try a pre-trained model for bacteria colony/fungus expansion prediction as the dynamics could be similar.
