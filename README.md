# Shorter-term-death-prediction workflow
# A deep learning workflow for predicting shorter-term death of acute kidney injury

The deep learning workflow can be used to predict the shorts-term death of AKI inpatients.

# Dependencies
You can install the required dependency library by requirement.txt. (Python 3.7 and TensorFlow 1.15)

# Data
Patient file format

For a patient, the csv files in the following format are needed for prediction. If value is unknow, you can leave the cell empty. (Please refer to the supplementary materials of the paper for specific data and types. The categorical variables need to be coded discretely.)

p1.csv
|T|	Variable 1|	Variable 2|	Variable 3|	……	|Variable N-1	|Variable N|
|-|-|-|-|-|-|-|
|t1	|					
|t2	|					
|t3	|				

Label file format

For all patients, a csv file in the following format is needed for prediction. (For different time window 24h, 48h, 72h and 7d, label should be corresponding death result.)

|File Name |Label|
|p1.csv|	0/1|
|P2.csv|	0/1|
|P3.csv|  0/1|

The patient data should be divided into derivation, internal validation, and external validation cohorts with corresponding label and put them to the directory /data.

# Train/Test
First, you should set the parameters in main.py, for example, the directory of data, batch_size, epoch, and so on. The mode should be set as “train”.

Second, you should set the number of class and input dimension (e.g., num_classes = 2, input_dim = 110) and modify the input dimension in the function of read_single_xlsx() in reader.py.

Third, you should comment the following code in main.py.
#extervalidation_data_path = os.path.join(args.data,'val/')
#extervalidation_label_path = os.path.join(args.data,'totalval.csv')
#extervalidation_data = data_load2(extervalidation_data_path , extervalidation_label_path, mode='train')
#random.shuffle(extervalidation_data)

Finally, you can conduct the train and test process.

# Validation
First, you should set the parameters in main.py, for example, the directory of data, batch_size, epoch, and so on. The mode should be set as “extervalidate”. The load_state should set as the path of trained model.

Second, you should set the number of class and input dimension (e.g., num_classes = 2, input_dim = 110) and modify the input dimension in the function of read_single_xlsx() in reader.py.

Third, you should comment the following code in main.py.
#derivation_data_path = os.path.join(args.data,'train/')
#derivation_label_path = os.path.join(args.data,'totaltrain.csv')
#derivation_data = data_load(derivation_data_path, derivation_label_path, mode='train')
#random.shuffle(derivation_data)

#intervalidation_data_path = os.path.join(args.data,'test/')
#intervalidation_label_path = os.path.join(args.data,'totaltest.csv')
#intervalidation_data = data_load2(intervalidation_data_path, intervalidation_label_path, mode='train')
#random.shuffle(intervalidation_data)

Finally, you can conduct the validation process.

# Evaluation
Evaluation code will analysis prediction by precision, recall, f-score, accuracy and AUROC.

The trained model and results are stored in output_save_path.

# Disclaimer
This model is for research purpose and not approved for clinical use.

