# API_final_project
In his project, we implement different methods for generating and converting the music style of the original music source. The technique we used is CycleGAN, RNN , VAE  and a few others provided by Magenta. So this project consists of the following components:
* music converter.ipynb: Workflow for the entire project, combining all the models.
* CycleGAN: Model of CycleGAN, and training process.
* Model_RNN.ipynb: The process of generating and training model RNN.
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

## RNN
Download the RNN file, the upload it on the Colab, after changing the source data path in the code, check to connect the GPU, finally you can click 'run all' or press keyboard 'Ctrl+F9' to train the RNN model.

## CycleGAN
first unzip CycleGAN.zip

We have run the model before, and you can directly go to directory named "test" and go to the bottom and in
the "mid" directory you can directly listen to the original midi file and transferred midi file that model has transferred.

If you want to train the model: 
copy datasets_cyclegan.zip into directory named "datasets" in CycleGAN and unzip it and 

## Model_VAE.ipynb
The file has the process of generating training dataset, creating and training model. We used 577 Jazz midi files to train VAE, the data can be found in [here](https://drive.google.com/file/d/1xksnOS46bODSO5KCXClWml62pFDMSVs2/view?usp=sharing). The saved VAE model can be found in [here](https://drive.google.com/drive/folders/1SxSvm-Sb2oyRVAC6BfBhctF5h8qmLsWc?usp=sharing).
