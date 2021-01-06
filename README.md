# DOSnet

Updated 11/19/2020 - By Victor Fung

This repo provides the code to run DOSnet, as detailed in the manuscript: Machine Learned Features from Density of States for Accurate Adsorption Energy Prediction. [1] DOSnet is a machine learning model which takes density of states as inputs to predict a targeted property such as adsorption energies. 

**Introduction:**

Materials databases generated by high-throughput computational screening, typically using density functional theory (DFT), have become valuable resources for discovering new heterogeneous catalysts, though the computational cost associated with generating them presents a crucial roadblock. Hence there is a significant demand for developing descriptors or features, in lieu of DFT, to accurately predict catalytic properties, such as adsorption energies. Here, we demonstrate an approach to predict energies using a convolutional neural network-based machine learning model to automatically obtain key features from the electronic density of states (DOS). The model, DOSnet, is evaluated for a diverse set of adsorbates and surfaces, yielding a mean absolute error of just 0.1 eV. In addition, DOSnet can provide physically meaningful predictions and insights by predicting responses to external perturbations to the electronic structure without additional DFT calculations, paving the way for the accelerated discovery of materials and catalysts by exploration of the electronic space.

**Usage:**

1. Install prerequisites listed in requirements.txt. You will need: \
Keras==2.2.2 \
numpy==1.14.3 \
scikit_learn==0.23.2

2. To run the code on existing examples provided here, first unpack the data file containing the DOS and energies: \
tar -xvf "your_file_here.tar.gz" \
or for the combined data: \
cat Combined_data.tar.gz.split* > Combined_data.tar.gz \
tar -xvf Combined_data.tar.gz

3. Run DOSnet: \
python Main.py \
Example: \
python Main.py --multi_adsorbate=1 --data_dir='Combined_data' --save_model=1 --batch_size=128

Output will be written to txt files as "predict_test.txt" or "predict_train.txt" or "CV_predict.txt" for a cross-validation run.

**Notes:**

1. For user generated training data, please note the data format for the ML input used here: \
-The surface and adsorbate DOS is saved as numpy arrays with shape (A, B, C) where A is number of samples, B is length of DOS file (2000 in the example), and C is number of channels.\
-Number of channels here is 27 for x_surface_dos which contains 9 orbitals x up to 3 adsorbing surface atoms. E.g. a top site will have the first 9 channels filled and remaining as zeros. This can be changed to individual specifications. \

2. The code can run on CPU or GPU depending on which resources are available and visible. If a GPU is available, it should be used automatically, but for more details consult the Keras documentation.

3. Model weights can be saved and loaded for transfer learning. A saved model is provided here as "DOSnet_saved.h5" which has been trained on approx. 37000 adsorption energies from Mamun et al. [2] Alternatively, they can be re-generated using the provided code and the "Combined_data" file containing the training data used.

4. Pytorch implementation forthcoming.

5. For any additional questions please contact Victor Fung at fungv(at)ornl.gov

**References:** \
[1] : Fung, V., Hu, G., Ganesh, P. et al. Machine learned features from density of states for accurate adsorption energy prediction. Nat Commun 12, 88 (2021) link: https://www.nature.com/articles/s41467-020-20342-6
[2] : Mamun, O., Winther, K.T., Boes, J.R. et al. High-throughput calculations of catalytic properties of bimetallic alloy surfaces. Sci Data 6, 76 (2019).
