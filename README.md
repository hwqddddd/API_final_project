# API_final_project
In this project, we implement different methods for generating and converting the music style of the original music source. The technique we used is CycleGAN, RNN , VAE  and a few others provided by Magenta. So this project consists of the following components:
* music converter.ipynb: Workflow for the entire project, combining all the models.
* CycleGAN: Model of CycleGAN, and training process.
* Model_RNN: Including the file of generating RNN model and the trained RNN model.
* Model_VAE.ipynb: The process of generating and training model VAE.
* Drums_RNN.ipynb: The process of generating and training model Drums_RNN, plus the generation of drum tracks using this model.
* Rhythm_based_drum_generation.ipynb: The process of generating and training model GrooVAE, plus the generation of drum tracks based on detected rhythms.


## music converter.ipynb
This code is used to combine all the trained together. The CycleGAN, or piano part, is not included because of the different tensorflow versions used. So before running this code, the path of the source midi and the generated midi for CycleGAN need to be checked.

More specifically, the parameters should be modified at 
`origin1 = pretty_midi.PrettyMIDI(YOUR_ORIGIN_PATH)`
, and 
`raw1 = load_midi(YOUR_TRANSFERED_PIANO_PATH)`.

Besides, the piano part should be transformed to MP3 file, to generate drum. The path should also be modified at `audio = "PIANO_PART.mp3"`

And all the models, including two folders for VAE and RNN, and the checkpoint for Drum Beats Generation should be download before running.

## RNN
Open file RNN, download the Model_RNN.ipynb file, then upload it on the Colab, after changing the source data path in the code, check to connect the Colab's GPU, finally you can click the botton 'run all' or press keyboard 'Ctrl+F9' to train the RNN model.

The file model_RNN.zip is the trained RNN model.

The training data can be found in [here](https://jazzomat.hfm-weimar.de/dbformat/dboverview.html).

## CycleGAN
- Environment setting:
python 3.6.13,
tensorflow 1.4.0,
numpy 1.19.5,
pretty_midi 0.2.8,
pypianoroll 0.1.3

First unzip CycleGAN.zip

We have run the model before, and you can directly go to directory named "test" and go to the bottom and in
the "mid" directory you can directly listen to the original midi file and transferred midi file that model has transferred.

If you want to train the model: 
copy datasets_cyclegan.zip into directory named "datasets" in CycleGAN and unzip it and then run the command as follow:
- Train a CycleGAN model:
```bash
python main.py --dataset_A_dir='JC_J' --dataset_B_dir='JC_C' --type='cyclegan' --model='base' --sigma_d=0 --phase='train'
```
If you want to directly test the model we have trained before:
download JC_J2JC_C_2022-12-05_base_0.0.zip from "https://drive.google.com/file/d/11ZSR0wVTu2PWjeZmd9KTl1UiIq_zPJkB/view?usp=sharing"
to directory"checkpoints" in CycleGAN and unzip it. then run the test command as follow:
- Test a CycleGAN model:
```bash
python main.py --dataset_A_dir='JC_C' --dataset_B_dir='JC_J' --type='cyclegan' --model='base' --sigma_d=0 --phase='test' --which_direction='AtoB'
```
After training, you can find sample midi in the directory named samples.
After testing, you can browse in directory named test, Go all the way to the bottom folder, enter the mid folder, which contains the midi file of the 
original test data(xxx_origin.mid) , the midi file used for the consistency loss calculation after the CycleGAN cycle(xxx_cycle.mid) and the final transferred 
midi file (xxx_transfer.mid), we have already run the test, so you can also directly choose to enter the folder "test/mid" to play these midi files to see the effect of the model.

Note: This CycleGAN model is refer to a project in Github(https://github.com/sumuzhao/CycleGAN-Music-Style-Transfer)


## Model_VAE.ipynb
The file has the process of generating training dataset, creating and training model. We used 577 Jazz midi files to train VAE, the data can be found in [here](https://drive.google.com/file/d/1xksnOS46bODSO5KCXClWml62pFDMSVs2/view?usp=sharing). The [saved VAE model](https://drive.google.com/drive/folders/1SxSvm-Sb2oyRVAC6BfBhctF5h8qmLsWc?usp=sharing) can generate new midi file.



## Drum Beats Generation
Our [jazz drum dataset](https://drive.google.com/drive/folders/1yZLWngJaPGHvzYkk1-NpkQiJE5bJePuF?usp=share_link) is extracted from the Groove MIDI Dataset. 
### For Drums_RNN.ipynb:
Use the given dataset to train the Drum RNN model and generate the drum tracks. This drum track can be exported as a MIDI file.
### For Rhythm_based_drum_generation.ipynb:
Use the given dataset to train the GrooVAE model. 
Alternatively, use the [pre-trained checkpoints](https://drive.google.com/drive/folders/1dVZJJV39-RuQaWFAPgRLkGIJAmHTiKT6?usp=share_link), together with the [piano audios](https://drive.google.com/drive/folders/1e5Em3_YSPlXW3_IEvppskGIqBFwzllTY?usp=share_link) to generate the drum beats. This drum track can be exported as a MIDI file.
