## Transfer Learning using Tensorflow
Dog Breed Identification using MobileNet. Make sure you have the latest version of tensorflow, execute this command: `pip install --upgrade tensorflow`

### Step 1
Download the images of dogs and labels from [here](https://www.kaggle.com/c/dog-breed-identification/data)

### Step 2:
Clone this [repo](https://github.com/googlecodelabs/tensorflow-for-poets-2). It contains the `scripts` directory which has helpers like `retrain.py` that we will use to re-train the last layer of the mobilenet on dog images.

### Step 3:
    cd tensorflow-for-poets-2 
    mkdir tf_files
    cd tf_files

### Step 4:
Copy the `organise_images.ipynb`, labels and images of dogs to `tensorflow-for-poets-2/tf_files` directory.  
`organise_images.ipynb` is a helper that will create sub-folders inside the `base_folder`. Each sub-folder is named after one of the categories and contains only images from that category.

### Step 5: 
Open the notebook: `organise_images.ipynb` using the command: `jupyter notebook` and update the following variables in the notebook:

    # Config
    LABELS = 'labels.csv'
    dogs_dir = 'dogs/'  #original dataset folder that contains pictures of dogs from all breeds
    base_folder = './dog_photos'

Run the notebook!

### Step 6: Re-train
Switch back to `tensorflow-for-poets-2/` directory

    python -m scripts.retrain \
    --bottleneck_dir=tf_files/bottlenecks \
    --how_many_training_steps=500 \
    --model_dir=tf_files/models/ \
    --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
    --output_graph=tf_files/retrained_graph.pb \
    --output_labels=tf_files/retrained_labels.txt \
    --architecture="${ARCHITECTURE}" \
    --image_dir=tf_files/dog_photos
 
 Substitute `${ARCHITECTURE}` with `mobilenet_1.0_224` and `--image_dir=tf_files/dog_photos` with `--image_dir=tf_files/{base_folder}`
 
 **Run the above command** and hopefully it will start training! For more [info](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/#3)
 
 ### Step 7: Testing the model on a image
    python -m scripts.label_image \
    --graph=tf_files/retrained_graph.pb  \
    --image=tf_files/{path_to_image}
 
 
