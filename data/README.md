# Data

The benchmark datasets (Trace, GunPoint, Plane) are fetched automatically from the UCR/UEA archive by `tslearn` and `pyts`. Nothing needs to be stored here for them.

Lab 1 (subsequence DTW) uses chroma features and audio from a commercial recording, provided with the course. They are **not** included in this repository for copyright reasons. To run that section, place these files in this folder:

```
StairwayToHeaven_1min_chroma.npy
StairwayToHeaven_MakesMeWonder_chroma.npy
StairwayToHeaven_1min.npy          # raw audio arrays (optional)
StairwayToHeaven_MakesMeWonder.npy # (optional)
StairwayToHeaven_1min.mp3          # for playback only (optional)
StairwayToHeaven_MakesMeWonder.mp3 # (optional)
```

Any pair of recordings works: extract 12-dimensional chroma features (for example with `librosa.feature.chroma_stft`) from a long recording and a short excerpt of it.

## Google Drive copy (for Colab)

Lab 1 in Colab downloads these files from a shared Google Drive folder. To set it up:

1. Create a folder in Google Drive, e.g. `dtw-to-attention-data`.
2. Upload the two chroma files (`*_chroma.npy`). The raw audio files are optional and are best not shared publicly.
3. Right-click the folder → **Share** → **General access: Anyone with the link** (Viewer) → **Copy link**.
4. Paste the link into `GDRIVE_FOLDER_URL` in the data cell at the top of `notebooks/01_dtw.ipynb`, then commit and push.
