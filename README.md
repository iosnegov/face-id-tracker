# Face ID Tracker: Real-Time Facial Recognition with CUDA Acceleration

*A real-time facial recognition pipeline, fully configured within an isolated Conda environment for effortless setup, reproducibility, and portability.*

## Available Documentation / Доступная документация

- [English Documentation](README.md) (current document / текущий документ)
- [Документация на русском языке](README_RU.md)

## Project Structure

```
face-id-tracker/
├── .env.example    # Configuration template
├── SBOMs/          # Dependency metadata
├── app/            # Application source code
└── photos/         # Input photo files
```

## Quick Start

### I. Prerequisites

| Component | Requirement |
| :--- | :--- |
| **Package Manager** | [`Micromamba`](https://github.com/mamba-org/mamba) |
| **Operating System** | GNU/Linux-based system |
| **Architecture** | `x86_64` |
| **Hardware** | NVIDIA GPU with a driver supporting CUDA >= 11.8 |
| **Development Tools** *(Optional)* | [`conda-lock`](https://github.com/conda/conda-lock) and [`pip-licenses`](https://github.com/raimon49/pip-licenses) |

> **Note:**  
> These are not strict requirements, but rather the baseline environment where the code is 
guaranteed to run out of the box. Alternative setups are possible but may require manual 
configuration.

### II. Clone the Repository

```bash
git clone https://github.com/snegoviol/face-id-tracker.git
cd face-id-tracker
```

### III. Create and Activate Virtual Environment

```bash
micromamba env create -p ./.venv -f SBOMs/conda-linux-64-lock.yml
micromamba activate ./.venv
```

### IV. Prepare Data

Add any photos to the `photos/` directory. The filename will be used as the person's name for recognition.  
For demonstration, you can download photos from [Pexels Free Stock Photos](https://www.pexels.com/).  
For example: [Man in brown polo shirt by Simon Robben from Pexels](https://www.pexels.com/photo/man-in-brown-polo-shirt-614810/).

### V. Configure via `.env`

1. Create `.env` file from template:

    ```bash
    cp .env.example .env
    ```

2. Edit `.env` in any text editor (e.g., `nano`, `VSCode`):

    ```bash
    nano .env
    ```

3. Configure parameters: the file is divided into sections — modify values according to your needs. For example:

    ```bash
    # === MODEL CONFIGURATION ===
    FACE_RECOGNITION_MODEL=hog
    FACE_DISTANCE_THRESHOLD=0.6

    # === DISPLAY SETTINGS ===
    CAMERA_INDEX=0
    CAMERA_WIDTH=1280
    CAMERA_HEIGHT=720
    RESIZE_FACTOR=2

    FONT=FONT_HERSHEY_COMPLEX
    COLOR_KNOWN=0,255,0
    COLOR_UNKNOWN=0,0,255
    COLOR_INFO=255,0,0

    # === PATH CONFIGURATION ===
    PHOTOS_DIR=photos

    # === LOCALIZATION SETTINGS ===
    UNKNOWN_PERSON_LABEL=Unknown
    TIMEZONE_OFFSET=0
    TIMEZONE_LABEL=UTC
    ```

### VI. Run the Application

```bash
python -m app.main
```

## License

Each file in this repository is licensed under the [MIT No Attribution License](LICENSE.txt).
