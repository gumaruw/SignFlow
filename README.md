# SignFlow — Sign Language Alphabet Recognition

## Overview

A system for recognizing English Sign Language letters from a webcam feed, using a CNN trained on a custom image dataset. Developed at Doğuş University as a Software Engineering course/team project to help explore how computer vision and machine learning can support sign language communication and learning.

## Project Structure
```
SignFlow/
├── data/, dataRenkli/, dataSag/, datamodelegitim/   - Training image datasets (per-letter folders)
├── gui.py              - GUI application for live recognition
├── egitim.py           - Training script (alternate version)
├── train_model.py      - Model training script
├── test_model.py       - Live webcam testing script
├── test.py             - Additional test script
├── requirements.txt
├── README.md
```

## Key Features
- **Real-Time Recognition:** classifies hand gestures from a live webcam feed.
- **CNN Model:** a Keras/TensorFlow convolutional network trained on a custom static-letter image dataset (24 classes: A–Y, excluding J and Z).
- **Data Augmentation:** random flips and rotations applied during training.

## Current Status

**Completed as a university course project (Oct 2024 – Feb 2025); not actively maintained since.** The code and known limitations below are left as-is from that point, rather than updated retroactively.

The trained model and the working recognition scripts (`gui.py`, `test_model.py`) classify the 24 **static** letters of the alphabet (J and Z are excluded, since they require hand motion rather than a single hand shape).

Separate image sequences for **J** and **Z** were collected (`data/J_frames`, `data/Z_frames`, `dataHareketli/`, including augmented variants), with the intent of eventually supporting these two dynamic gestures. That integration was not completed — the dynamic-gesture data exists in the repository, but the trained model and deployed scripts do not use it.

Accuracy was assessed by observing predictions during live testing rather than through a logged/benchmarked evaluation run: across repeated live tests, the model correctly recognized letters roughly 90%+ of the time. No formal train/val/test benchmark was run, so treat this as an informal, observed figure rather than a measured metric.

## Technical Details
- **Framework:** TensorFlow / Keras
- **Language:** Python
- **Libraries:** OpenCV, NumPy, tqdm
- **Model:** Convolutional Neural Network (Conv2D + MaxPooling ×3, Dense, Dropout), 128×128 input images
- **Dataset:** custom static-letter image dataset

## How It Works
1. **Input:** capture a frame from the webcam.
2. **Preprocessing:** resize to 128×128 and normalize.
3. **Prediction:** the trained CNN classifies the frame among the 24 static letters.
4. **Output:** the predicted letter is overlaid on the live video feed.

## Installation & Usage

```bash
git clone https://github.com/gumaruw/SignFlow.git
cd SignFlow
pip install -r requirements.txt
```

Train a model:
```bash
python train_model.py
```
(Note: `train_model.py` and `egitim.py` both contain a hardcoded local dataset path — update `DATASET_PATH` to point to your own copy of the training images before running.)

Run live recognition:
```bash
python test_model.py
```
(Requires a saved model file, e.g. `sign_model_epoch_5.h5`, produced by `train_model.py` — not included in this repository.)

## Known Limitations
- Only the 24 static letters are recognized; J and Z are not yet supported by the trained model.
- No accuracy has been formally logged or benchmarked — only observed during manual testing.
- Training scripts contain hardcoded local file paths.
- Trained model weights (`.h5` files) are not included in the repository.
- `gui.py` and `test_model.py` are separate, not-fully-unified entry points (no single `main.py`).

## Goals
- Support easier communication for hearing-impaired individuals.
- Serve as an educational tool for learning sign language.
- Explore accessible, low-cost computer-vision approaches to gesture recognition.

## Contributors
- Ayşe Ceren Doğan
- Cemre Dağ
- Emir Ekrem Kaya
- Hatice Uçar
