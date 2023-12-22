# LFBNet3D

To train the model from a new dataset, change to the ai4elife/src directory:


python train.py --input_dir path/to/training_validation_data/  --data_id <unique_data_name> --task <train>


To evaluate on the validation data:

python train.py --input_dir path/to/validation_data/  --data_id <unique_data_name> --task <valid>
