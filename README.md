# CS294-082-Final-Project
CS 294-082 Multimedia in Machine Learning Final Project


### Part 1: Dataset generation
The first part of the project is generating the dataset. We open the retinal image 20205_map.png and generate croppings according to the patch_size and stride. 

Afterwards, we pass our cropped images through a pretrained ResNet50 model to generate deep features and save the output as a csv file. 

We begin by splitting the dataset into train and test sets. These datasets can be found in data.zip.


### Part 2: MEC Calculation
The second half of the project is MEC calculation. We calculate the dataset MEC using the train set only by implementing Algorithm 1 from Chapter 9 of the “An Information View on Data Science” textbook.

We then create the capacity plot by using the output of Brainome (brainome [retina_data_train.csv file path] -y -o [output name] -f NN -split 80 -e 5) and translating its units of decision points into bits of information.

We then proceed to training for memorization. We create an sklearn MLPClassifier whose hidden size layer is large enough for the network's MEC to match the dataset's MEC as calculated earlier. We then confirm that the accuracy on the training set is near 100% after training.

We then train for generalization. We perform an 80/20 split the training set to create a validation set and test neural network architectures with a single hidden layer. Hidden neurons are added incrementally until the model's MEC is equivalent to the dataset MEC. We then plot the training and validation accuracies relative to model MECs in order to determine N_approx, the model MEC that we should choose for our final model.

We then train a neural network using the N-approx value on the entire training set and evaluate its performance on the test set.
