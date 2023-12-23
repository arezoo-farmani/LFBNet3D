
# 3D version 
# AI4eLIFE: Artificial Intelligence for Efficient Learning-based Image Feature Extraction.

# Required folder structure
Please provide all data in a single directory. The method automatically analyses all given data batch-wise.

To run the program, you only need PET scans (CT is not required) of patients in nifty format, where the PET images are coded in SUV units. If your images have already been segmented, you can also provide the mask (ground truth (gt)) as a binary image in nifty format. Suppose you provided ground truth (gt) data; it will print the dice, sensitivity, and specificity metrics between the reference segmentation by the expert (i.e., gt) and the predicted segmentation by the model. If the ground truth is NOT AVAILABLE, the model will only predict the segmentation.

A typical data directory might look like:

|-- main_folder                                             

|      |-- parent folder (patient_folder_1)             
|           |-- pet                                     
                 | -- name.nii or name.nii.gz            
|           |-- gt                                      
                 | -- name.nii or name.nii.gz            
|      |-- parent folder (patient_folder_2)             
|          |-- gt                                     
                | -- name.nii or name.nii.gz            
|         |-- pet                                      
                | -- name.nii or name.nii.gz            
|           .
|           .
|           .
|      |-- parent folder (patient_folder_N)            
|           |-- pet                                   
                | -- name.nii or name.nii.gz           
|           |-- gt                                      
                | -- name.nii or name.nii.gz           
                
Note: the folder name for PET images should be pet and for the ground truth gt. All other folder and sub-folder names could be anything.

⚙️ Installation
Please read the documentation before opening an issue!

Download/clone code to your local computer

- git clone https://github.com/arezoo-farmani/LFBNet3D.git

- Alternatively:
  1. go to https://github.com/arezoo-farmani/LFBNet3D.git >> [Code] >> Download ZIP file.
To install in virtual environment

We recommend you to create virtual environment. please refer to THIS regarding how to create a virtual environment using conda.

Open terminal or Anaconda Prompt


Change the working directory to the downloaded and unzipped ai4elife folder


Create the virtual environment provided in the requirements.yaml:

conda env create -f environment.yml


If you choose to use a virtual environment, the virtual environment must be activated before executing any script:

conda activate myenv


Verify the virtual environment was installed correctly:

conda info --envs

If you can see the virtual environment with a name 'myenv', well done, the virtual environment and dependencies are installed successfully.

Using docker image: building image from docker file [REPRODUCIBLE]


Assuming you already have docker desktop installed. For more information, kindly refer to THIS.

Make sure to change the directory to the downloaded and unzipped ai4elife directory.


Run the following commands to create a docker image with the name :'


docker build -t <DockerImageName>:<Tag> .

💻 Usage
This package has two usages. The first one is to segment tumor regions and then calculate the surrogate biomarkers such as sTMTV and sDmax on the given test dataset using the pre-trained weights, named as "easy use case". The second use case is transfer learning or retraining from scratch on your own dataset.

Easy use: testing mode
Please make sure that you organized your data as in the Required folder structure.

For reproducibility and better accuracy, please use OPTION 2.
Option 1: Using the virtual environment:


Change to the source directory: cd  path/to/ai4elife/


Activate the virtual environment: conda activate myenv


Run: python test_env.py  --input_dir path/to/input/  --output_dir path/to/output/


Option 2: Using the docker:


Option 1:run_docker_image.bat path/to/input path/to/output  <docker_image_name> <Tag>  <container_id>

Option 2: docker run -it --rm --name <container_id> -v path/to/input/:/input -v path/to/output/:/output <docker_image_name>:<Tag>


Transfer learning mode: development
To apply transfer learning by using the trained weights or training the deep learning method from scratch, we recommend following the virtual environment-based installation option.

Run the following commands for activating the virtual environment, and then training, validating, and testing of the proposed model on your own dataset.

Activate the virtual environment: conda activate myenv


# To train the model from a new dataset, change to the LFBNet3D/src directory:


python train.py --input_dir path/to/training_validation_data/  --data_id <unique_data_name> --task <train>


# To evaluate on the validation data:

python train.py --input_dir path/to/validation_data/  --data_id <unique_data_name> --task <valid>


Note: You can also configure the deep learning model for parameter and architectural search. Please refer to the documentation configuration. Briefly, you can apply different features, kernel size in the convolution, depth of the neural networks, and other hyperparameters values. The segmentation model is designed in easy configurable mode.





To train the model from a new dataset, change to the LFBNet3D directory:

python train.py --input_dir path/to/training_validation_data/  --data_id <unique_data_name> --task <train>

To evaluate on the validation data:

python train.py --input_dir path/to/validation_data/  --data_id <unique_data_name> --task <valid>
