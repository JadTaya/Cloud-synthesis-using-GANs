The dataset and the DCGAN model can be found [here](https://drive.google.com/drive/u/0/folders/1hTgTmXlIXD9AxxfdW-O9wyOn5gHck-7d).
If you wanna run the code, you need to add the dataset files and create 2 empty folders with the names "results&models" and "runs".

# Cloud-synthesis-using-GANs
You can find the final paper up above.

"2D_zeroPadaed_clouds_orig" is the whole dataset that we exported from pyshdom.

A lot of the code is based on "DCGAN tutorial", reading it can help you understand the code in the notebooks "dcgan_clouds_complete" and "wgan_clouds_prio_dist".
https://pytorch.org/tutorials/beginner/dcgan_faces_tutorial.html

Also the WGANGP article to understand the WGAN code.
https://arxiv.org/abs/1704.00028


The notebook "dataset_stats" has the code to split the dataset into training and test sets, and also some code to run some statistics on both sets.
Some of the results of running the code can be found in the folder "dataset" while for others you'll need to run the code, since they're too big to send/upload.


The notebooks "dcgan_clouds_complete" and "wgan_clouds_prio_dist" run the training process for both GANs, a lot of the code can be explained be reading the DCGAN tutorial.
In cell (14) in the dcgan code and cell (18) in the wgan code (the training loops), the code will automatically create a directory inside "/results&models" every run,
 if no parameters mentioned in "dir_name" have been changed since the last run then it won't start and will give you an error, so do with that information as you wish,
you can either find a better way to automatically do this or just manually change the name every run. The purpose of this directory is to save the generator and
discriminator models every epoch, a sample of the results is saved in "\results" and the models are saved in "\models".

Also the code supports adding tensorboard scalars, simply add the scalars you wanna observe each epoch just like the scalars already present in the code,
run a terminal in your current environment, change the directory "cd" to where the "\runs" folder is, and use the command "tensorboard --logdir=runs",
finally go to "http://localhost:6006/" in your browser. 
check out 
https://pytorch.org/docs/stable/tensorboard.html
for further info.


The notebook "compare_stats" uses the generator models that were saved in the training process (in the directory results&models\...\models\) to generate random results from 
the epoch range chosen in cell (14) and compare them to the test dataset.
For example currently you can see in the notebook the epoch range 198-200, the models are found in the directory "\WGAN_prio"
In cell (13) you can see the relevant code that you might need to change if you wanna run this code on different models:
test_netG.load_state_dict(torch.load('WGAN_prio/G-{}.pt'.format(model_num)))

