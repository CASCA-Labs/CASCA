# CASCA Access Request

This repository is private and requires access approval. Please request access.

## Request Access

Please fill out the form at the following link to request access:
[Request Access Form](https://forms.gle/o24kTRv8TmWArpos6)

## Process

We will review your request and grant or deny access within 24 hours. Thank you.

# About CASCA

**CASCA - Context Aware Speech Classification Architecture** - is an integrated speech diarization system that uses role information to facilitate turn-level speaker assignment. CASCA is versatile, requiring no prior information of speaker identities, and robust, applicable even in cases of weak speaker role differentiation. Currently, diarization is limited to conversations of two speakers.


## Installation

1. Clone repo
```bash
  git clone https://github.com/CASCA_Labs/CASCA_Source.git
  cd CASCA
```
2. Create venv and install dependencies:
```bash
  conda create -n casca-env python=3.9
  conda activate casca-env
  git clone https://github.com/microsoft/UniSpeech.git
  pip install --no-deps -r requirements.txt
```
3. Download WAVLM embeddings model and input data [here.](https://drive.google.com/drive/folders/15j3NRQEaBuj3J7CnC2qh11cMWos-hZMF?usp=sharing)

4. Model weights are served from predibase. Access them [here.](https://app.predibase.com/auth/signup?token=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpbnZpdGVySUQiOjI5NTMsImludml0ZWUiOiJnbG9iYWwiLCJyb2xlSUQiOjMzNzIsInRlbmFudFVVSUQiOiI1YTNkMTdkYi1hZGRjLTRkZTAtOTM3OC1hZTI2Yjk0MzFhOWYiLCJJc1N5c3RlbVNpZ251cCI6ZmFsc2UsImV4cCI6MTcxNTYzNjM4NCwiaWF0IjoxNzEzMDQ0Mzg0LCJpc3MiOiJwcmVkaWJhc2UiLCJuYmYiOjE3MTMwNDQzODQsInN1YiI6IjVhM2QxN2RiLWFkZGMtNGRlMC05Mzc4LWFlMjZiOTQzMWE5ZiJ9.QA7NjS3r8Z2Pc_8TXm5DGMeifTtQ9ZP-Q11sh7IWrtxwof31FbNWPT8JZL55j926wNx2IZjESOBlKp6QGc4QXb3jFS7C61GJhz2D77-1jvQrhLZeoFI6cU2Pmu6qe6quXD8zcJBjuv9Rve3yh4uTo1RhrkAGF-h_YrcioioksarfI_6nnSeu5vaBAUSomhPTo5CtI01WKe0iHehiKOFZjTcQWnZwZpOdf_LN9zDiQKBs-VaqmywSDYOBtGNgVTOVFHr1qPKxl3YWyr0oSNLWLP9BpywCDc6WPnmfImYZBRZTqEKQ9MrDVwmC_R2_6DuCAY8fVSS1c4SOS763S7qk2Q)


## Usage

 Run the `casca.py` script with the desired options:

### Options

- `--input_path INPUT_PATH`: File or directory to diarize.
- `--output_dir OUTPUT_DIR`: Output directory (defaults to `final_outputs/` if not provided).
- `--wder`: Evaluate diarization word error rate for the target file.
- `--identify_speakers`: Automatically assign a descriptive name to speakers using role information. Otherwise, speakers will be labeled as Speaker_01, Speaker_02, etc.
- `--roles`: Assist role assignment with context of conversation(s).
- `--post_process`: Post-process transcript using contextual cues to reassign speech segments of uncertain label.
- `--rerun_transcription`: Rerun transcription (default: true).
- `--rerun_role_pipeline`: Run role pipeline (default: true).
- `--simple_transcript`: Output transcript in the format of "Speaker: Text" instead of the default full RTTM format.

### Examples

1. Diarize a single file and output the results to the default `final_outputs/` directory:

    ```bash
    python casca.py --input_path /path/to/your/file.wav
    ```
2.  Diarize all files in directory `audio/` and output to  `transcripts/` directory:

    ```bash
    python casca.py --input_path /path/to/audio/ --output_dir transcripts/
    ```
3. Automatically name speakers based on conversation roles and correct low confidence speaker turns(experimental)
    ```bash
    python casca.py --input_path /path/to/audio/ --output_dir transcripts/ --identify_speakers --post_process
    ```

## Replicating Results

### Overview
This section provides instructions to replicate the experiments presented in our Interspeech 2024 paper titled "CASCA: A General Framework for Leveraging Speaker Role Information in Speech Diarization."

Download the TalkBank test set and corresponding rttms [here.](https://drive.google.com/drive/folders/15j3NRQEaBuj3J7CnC2qh11cMWos-hZMF?usp=sharing)


Run
    ```
    python casca.py --input_path input_data/ --wder
    ```
    

## Cite this project
If you use CASCA for your research or if you refer to this repository in your work, please cite it using the following format:

```plaintext
@inproceedings{2024casca,
  title={CASCA: A General Framework for Leveraging Speaker Role Information in Speech Diarization},
  booktitle={Interspeech 2024},
  year={2024},
  organization={CASCA Labs}
}
```

## Acknowledgements

 - [WhisperX](https://github.com/m-bain/whisperX)
 - [MeetEval](https://github.com/fgnt/meeteval)




