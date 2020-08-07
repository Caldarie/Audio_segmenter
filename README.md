# Audio Segmenter
Python script to splice audio files to 5 second intervals, as well as normalize amplitude, channel, sampling rate; and lastly removing unnesscary silences. Used to preprocess raw audio data for machine learning

## If you need to splice silences:
1. Open parameter_tester.ipynb to test and find the optimal silence length and threshold.
2. Run the first cell to splice a sample of your original raw audio data.
3. Adjust the parameters in `nonsilent_data = detect_nonsilent(normalized_sound, min_silence_len=4000, silence_thresh=-32, seek_step=1)`, then run the cell
4. Run the third cell to output wave graph. 
5. Using the wave graph, make sure that it matches with the time frame from the second cell. If it doesn't match, readjust the parameters again.

