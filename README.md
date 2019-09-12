# NER_RNN_mine

Inintian NER_RNN provide the functionality to name-entityi recognition problem.
The proposed approcahes are:
birnn
cfr- word-level embeddings
cnn- char-level embeddings and convolution under it
cnn-cfr - concatenation of word-level and char-level embeddings(with convolution)

You can see the details in src/model/*model_name*.py in forward function.

The model provides seq_indexer class to map word or char to indexes for subsequent submission to the model input.

I replace 2 layer of cnn-cfr by elmo layer from allenlp module.

As *allennlp* provide its own indexing, seq_indexer is disabled. Also elmo requires input not according to words, but according to sentences (since embedding is determined from the context).
Elmo object is created when create object of corresponding model (in main.py "isElmo" flag goes to model factory) 

run as 
python3 main.py --train path_to_train --dev path_to_dev --test path_to_test --data-io connl-ner-2003 --evaluator f1-alpha-match-10 --model BiRNNCRF --opt adam --lr 0.001 --save-best yes --patience 20 --rnn-hidden-dim 200 --gpu 1 --save model_name

dev-train-test for aspects are in https://drive.google.com/drive/folders/1JpNmpbBGVwt081xptY7ZPKRTjQnwFyeU?usp=sharing