# Genre_Synthesis
A repository including the architecture and datasets used for speech genre synthesis.

## Overview
A Speech Genre is defined as a categorisation of speech based on the type of function the text holds, and the
manner of speech which is associated with the function. A Speech Genre consists of two entities, a
Speech Function, and a Speech Register. A Speech Function is a piece of text from which the characteristics are derived from a specific context
and application, which usually bear socially agreed upon conventions. It is generally consistent on
the level of thematic content, but may differ in terms of individual aesthetic preferences. A Speech Register is a manner of speech which is governed by its functional communicative context,
taking into account both the function of the given speech, alongside any stylistic choices made by the
speaker.

The architecture used for Genre Synthesis is modular. The benfit of this approach is that you can replace any of the components with a different architecture (which, the more in the future it is, the better it probably is.
In this particular research paper, 4 genres were synthesised: TEDTalk, Documentary, News Broadcast, and Stand-Up Comedy. Each genre was subsequently split according to the gender of the speaker. Naturally, more are possible.

## Walkthrough
The process of synthesising Speech Genres is as follows:

1) First, a piece of text needs to be converted into neutral synthesised speech (speech which is devoid of any Speech Register) using a speech synthesiser. In this research paper, FastSpeech2 is used for this task. Inside the FastSpeech2 folder
is a notebook file which contains the git clone command for the specific implementation of FastSpeech2 used. There is both a README file inside of this folder, and a README file from the cloned folder. Follow the
instructions of those README files (download the pretrained model). To synthesise desired text, the input was changed within the eval.py file. The folder contains both text with the Speech Function of each genre (Reference Audio
Text) and function neutral text (Harvard Sentences), both of which were used in the research paper.
2) Secondly, a text classifier is required to identify the Speech Function of a given text. This task is performed by a Recurrent Convolutional Neural Network (RCNN) in this research paper. Inside of the RCNN folder, there is a notebook file which
contains the git clone command to the specific RCNN implementation used. Follow the instructions of the README file inside of that folder. The README file contains a link to a zipped folder which contains the
necessary csv files to train the RCNN models used in the research paper, alongside the classes.txt necessary for classification. You unzip this folder and use the contents to replace the files from the default
git clone. The cloned repository has the tools to both train and evaluate the RCNN models.
3) Finally, the k-Nearest Neighbours Voice Conversion (kNN-VC) architecture is used to apply the Speech Register to the output of the speech synthesiser from step 1. Inside of the kNN-VC folder is a notebook file which
contains the torch.hub.load() call of the kNN-VC architecture, alongside the full implementation of creating the Speech Register embeddings, and applying them to speech samples. The folder containing all of the audio files
is too large to be included. Thus, the README file contains a link to a zipped folder which contains the PyTorch tensors for each of the genres, for each of the genders. 

With these steps, you should be able to synthesise Speech Genres. The research paper also looked at alternative cases where the Speech Function did not match the Speech Register (e.g. a News Broadcast text being
synthesised with a Stand-Up Comedy register) or the synthesis of function neutral text with various registers.

## Additional Material
*Embeddings - Subset* - A folder which contains a small subset of the training data used for the kNN-VC to generate the genre embeddings.

*PsyToolKit Script* - A folder which contains the survey file used for the evaluation of synthesised speech samples. The Samples folder contains the necessary samples required to run the survey.

*Result_Analysis* - A folder which contains the notebook files which analysed both the RCNN evaluation, and the human evaluation of synthesised speech samples. The accompanying data.csv file contains the responses of all
of the participants, each indexed with a unique but nontraceable key.

*Web Scraping Tools* - A folder which contains the notebook files which were used to obtain the text necessary to train the RCNN, one for each genre. Additionally, the Text Splitter notebook is used to split the text for each genre into
segments of texts of desired character length.

*Additional Figures* - Figures of results which couldn't make it into the main document. Most of them are genre specific breakdowns of each question.

