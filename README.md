# Audio Segmentation
The scripts uses a modified pydub package (0.24.1) to segment and normalize raw conversational/speeches files for machine learning. Compared to using the standard pydub library, this script is optimized for processing audio by removing the need to use multiple loops to segment data.

Please be aware that this script can/may be broken if any other pydub versions are used.

## audio_segmentation.ipynb

This script assumes that there is only one speaker. If you need to find the optimal silence threshold and length, please use 'parameter_tester.ipynb' to find the optimal values.

What this script will do is:
  1. Removes unnecessary long pauses/silences, but retaining natural silences which indicates the speakers thoughts or use of fillers.
  2. Splits the audio files into 5 second intervals. Files that are too short will be kept but labelled as "leftover"
  3. Normalize amplitude, chanhel, and sampling rate.
  4. [Future Feature] Removes background noise if applicable
  5. [Future Feature] Generates a unique adds id for each file

## convert.ipynb

This script is used to process audio data where there are two speakers. 

What this script will do is:
  1. Convert the files to wav
  2. After editing out the interviewer with audacity, normalize the audio
  3. Splice the spliced files into 5 second interval
  4. Retains files that are under 5 seconds and appends as leftover
  5. [Future Feature] Generates a unique adds id for each file

## create_dataframe.ipynb

Iterates wav files and creates a metadata.

What this will do:
  1. Records the name of the file
  2. Records the sub folder location 
  3. Records the audio data in a float 32 numpy array (used for tensor input)
  4. Records the sample rate as a int32 numpy array (used for tensor input)
  5. Records length of audio file 
  6. Records the bit depth of audio file
  

## parameter_tester.ipynb

If you need to find the optimal parameters for removing silence in your audio.

1. Open parameter_tester.ipynb. This script will take a sample of your original file, which can be used to test and find the optimal silence length and threshold.

2. Run the first cell to splice a sample of your original raw audio data.

3. Adjust the parameters in `nonsilent_data = detect_nonsilent(normalized_sound, min_silence_len=4000, silence_thresh=-32, seek_step=1)`, then run the cell. It should output a series of time frames, for example:

![Time frame](https://github.com/Caldarie/Audio_segmenter/blob/master/Images/Screen%20Shot%202020-07-31%20at%209.39.55%20pm.png)

4. Run the third cell to output wave graph. 

5. Using the wave graph, make sure that it matches with the time frame from the second cell. If it doesn't match, readjust the parameters again. Optimal parameters should match the time frames like this:
![Wave Graph](https://github.com/Caldarie/Audio_segmenter/blob/master/Images/Screen%20Shot%202020-07-27%20at%2011.04.38%20pm.png)

  

