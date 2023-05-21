# cs6910_assignment3
seq2seq transliteration

The train.py file have args pass parameter and one can set the values such as encoder dropout , decoder dropout, hidden layer size .etc below are the mentioned parameter then one can pass along 
"-wp"   "--wandb_project"         for wandb project name      
"-we"   "--wandb_entity"          for wandb entity name
"-e"    "--epochs"                for number of epochs
"-b"    "--batch_size"            for batch size
"-emb"    "--embedding_size"      for embedding size
"-ct"   "--cell_type"             for cell type choice is there "RNN","GRU","LSTM"
"-attn"   "--attention"           if attention is required or not 
"-sz"   "--hidden_size"           size of the hidden layer
"-nhl"    "--num_layers"          number of layers in encoder and decoder
"-dpe"    "--dropout_encoder"     dropout value for encoder  
"-dpd"    "--dropout_decoder"      dropout value for decoder
"-bd"   "--bidirectional"         True or False value 

by default the value are kept for the best accuracy model and the argpass part is commented as if we run the code on kaggle it will give error so if you run the code in your local and want to pass the argument please uncomment the line no 28-56   , 184-199 , 737 and 788 after uncommenting these lines certain lines have to be commented
60-62 , 165-180 , 734, 786 


if running the code in local please keep the the dataset at the directory from where the code is running with the unzip version 'aksharantar_sampled'



2>if running code in kaggle please add the dataset aksharantar_sampled and name it as aksharantar 
#how the Model is trained 
First we prepare the data for doing this we import the dataset as dataframe using pandas 
we then prepare vocabulary of both input and output language in our case english and hindi
after the dictionary is built sucessfully we created class of encoder and decoder 
then the input words which are in english are converted to tensor's these tensor are then group together to form a batch 
the batch is then passed through the encoder and the output from the last hidden layer of encoder is sent as input to hidden layer of decoder 
in decoder we then pass start of token to the first cell and latter using teacher forching for 50% of the time either ground truth is fed to the next decoder cell input or the current output is fed , once the whole batch is processed it is returned .
now we calculate loss and do backward propogation to adjust the weights , once this is done we calculate the accuracy on valid dataset we keep on doing the process 
now for the best configuration obtained we apply this model on test dataset and capture the translated words and the test accuracy 

similar process is done for the model with attention but instead of looking at the whole encoded input at once it priority are given to letters with higher attention 
weights in the decoder , so this help in improving the accuracy of translation when it comes to words that sound similar and for vowels .






