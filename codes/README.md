# THIS FILE DOES NOT CONTAIN ANY MODELS, IF YOU WANT THE VERSION WITH MODELS, PLEASE DOWNLOAD THE ZIP FILE IN THIS LINK:
https://drive.google.com/file/d/1MpJu8xkiJKIVyO5_T44nwvry_7RnNpEL/view?usp=sharing

# Important! If you just want to read the reports:
1. all the .out files are reports for different models based on caffe.
    a. Original caffe model, trained 10 epochs and 20 epochs each: original_report_10_epochs.out and original_report_20_epochs.out
    b. Removed the third convolutional layer from orginal: one_conv_less_report.out
    c. Removed the third convolutional layer and a fully connected layer from orginal: reduced_both_report.out 
    d. Only 1 convolutional layer and 1 linear layer: gender_min_report.out
    e. Split adience into 16 catecories: split_report.out
    f. Unweighted age head and gender head: age_gender_report.out 
    g. 1 gender head and 8 age heads, with weights and age encoding: gender_with_new_age_encode_report.out
    h. Pretrain on CELEBA: celeba_report.out
    i. Finetune on ADIENCE: pretrained_report.out

2. The graph output are all under graph folder.

3. The models based on ResNet34 are in the folder "notebook"

# If you want to train the models yourself (Caffe version):
Warning: doing so will replace the .out report. It is advised to make a copy of all files before retraining.

0. Install PyTorch (CUDA 11.3 version)
1. Check that test.json, train.json, and valid.json are under the 'aligned' folder. The rest of that folder should be ADIENCE's inner folders, such as 7153718@N04.
2. Change the PATH on aggender_dataset.py to the one leading to your 'aligned' folder.
    e.g. PATH = 'aligned/'
3. Select a model that you want to train, and find its python file:
    1. Modify caffe models, the output will be under "gender_model" folder.
        a. original_output.py (original caffe model)
        b. one_conv_less.py (remove the third convolutional layer from above)
        c. reduced_both.py (remove the third convolutional layer and a linear layer)
        d. gender_minimalist_output.py (only 1 convolutional layer and 1 linear layer)
    2. Joint classification of age and gender
        a. age_gender_split.py (split adience into 16 catecories), model output will be in "gender_model/split".
        b. age_gender_output.py (1 age head and 1 gender head), model output will be in "agegender_model".
        c. gender_with_new_age_encode.py (1 gender head and 8 age heads), model output will be in "gender_with_new_age_encoding".
    3. Pretrain on CELEBA then ADIENCE
        a. Place CELEBA into a folder "celeba". There two files, attr.txt and partition.txt, under it. The rest of that folder should be img_align_celeba, a folder where all pictures are inside.
        b. Copy the folder path to celeba_output.py, replace img_folder. e.g. img_folder = f'celeba', where inside celeba you can find img_align_celeba, attr.txt and partition.txt.
        c. Run "nohup python3 celeba_output.py > celeba_report.out", model output will be in"celeba_model".
        d. pretrained_on_adience.py (finetune the above model on ADIENCE), model output will be in "gender_model/finetune".
4. replace the open("....") with the path to your json file on the previously selected python file.
    e.g.
    train_label=np.array(list(json.load(open("aligned/train.json")).items()))
    valid_label=np.array(list(json.load(open("aligned/valid.json")).items()))
    test_label=np.array(list(json.load(open("aligned/test.json")).items()))

5. Find the corresponding command on "my command.txt" and copy it to console.
6. See your report at the .out file. The graphs can be found in the graph folder, and the trained model under its respective folder.


# For ResNet34:
ADIENCE dataset link: 
https://drive.google.com/drive/folders/1rzp8qdsuDFx6kuZYbqkmycUmoYkJjnv8?usp=share_link

1. All notebooks are developed in google colab environment. In colab, run the first cell in every notebook to install required packages
2. Run the notebooks found under notebook folder. The saved models are under notebook_saved_models.
| Model ID in report | Model name in folder |
| ------ | ------ |
| ResNet trained on CELEBA | ResNet_celeba.h5 |
| 9 | celeba_age_gen_base.h5 |
| 10 | celeba_age_gen_plus.h5 |
| 11 | celeba_modified_age_gen_base.h5 |
| 12 | celeba_modified_age_gen_plus.h5 |
| 13 | full_celeba_modified_age_gen_base.h5 |
| 14 | full_celeba_modified_age_gen_plus.h5 |