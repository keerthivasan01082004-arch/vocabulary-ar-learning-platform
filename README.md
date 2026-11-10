# Vocabulary AR Learning Platform

A Django-powered augmented-reality vocabulary learning platform that combines real-time object detection, multilingual translation, pronunciation support, handwriting recognition, and gesture-based writing practice.

The application uses a webcam to identify everyday objects, displays their vocabulary in a selected language, and turns recognition into an interactive learning activity.

## Highlights

- Real-time object detection using YOLOv5 and OpenCV.
- Multilingual vocabulary translation for Indian and international languages.
- Pronunciation and transliteration support for translated words.
- Browser-based webcam experience served through Django.
- Handwriting practice with OCR-based answer checking through Tesseract.
- Gesture-based writing practice using MediaPipe hand tracking.
- Learning scores stored through Django models and migrations.
- Responsive templates for detection, word lists, translations, handwriting, and gesture practice.

## Learning workflow

```text
Webcam frame
    ↓
Object detection with YOLOv5
    ↓
Recognized object and vocabulary lookup
    ↓
Translation · pronunciation · transliteration
    ↓
Handwriting or gesture-based practice
    ↓
OCR / gesture validation and learning score
```

## Technology stack

- **Backend:** Python, Django
- **Computer vision:** YOLOv5, Ultralytics, OpenCV
- **Gesture recognition:** MediaPipe
- **Handwriting recognition:** Tesseract OCR through `pytesseract`
- **Translation:** `deep-translator`
- **Language support:** Indic transliteration utilities
- **Frontend:** Django templates, HTML, CSS, JavaScript
- **Database:** SQLite for local development through Django ORM

## Project structure

```text
vocabulary-ar-learning-platform/
├── events/
│   ├── migrations/       # Database migrations
│   ├── static/           # Application stylesheets
│   ├── models.py         # Detected objects and learning scores
│   ├── urls.py           # Application routes
│   └── views.py          # Detection, translation, OCR, and gesture workflows
├── templates/
│   ├── index.html        # Landing page
│   ├── det.html          # Detection interface
│   ├── list.html         # Detected vocabulary list
│   ├── translation_detail.html
│   ├── handwriting_test.html
│   └── gesture_write.html
├── voc/
│   ├── settings.py       # Django project configuration
│   ├── urls.py           # Root URL configuration
│   ├── asgi.py           # ASGI entry point
│   └── wsgi.py           # WSGI entry point
├── yolov5s.pt            # YOLOv5 model weights
├── manage.py
├── requirements.txt
└── README.md
```

## Installation

### 1. Clone and enter the project

```bash
git clone https://github.com/keerthivasan01082004-arch/vocabulary-ar-learning-platform.git
cd vocabulary-ar-learning-platform
```

### 2. Create a virtual environment

```bash
python -m venv .venv

# macOS/Linux
source .venv/bin/activate

# Windows PowerShell
.venv\Scripts\Activate.ps1
```

### 3. Install Python dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Install Tesseract OCR

Handwriting validation uses Tesseract. Install the Tesseract executable for your operating system and make sure it is available on your system `PATH`.

- Ubuntu/Debian: `sudo apt install tesseract-ocr`
- macOS: `brew install tesseract`
- Windows: install Tesseract and configure its executable path if it is not added to `PATH`

### 5. Apply database migrations

The repository intentionally excludes the local SQLite database. Create it from the committed migrations:

```bash
python manage.py migrate
```

### 6. Start the development server

```bash
python manage.py runserver
```

Open `http://127.0.0.1:8000/` in a browser and allow camera access when prompted.

## Main application routes

| Route | Purpose |
|---|---|
| `/` | Vocabulary learning landing page |
| Detection routes | Webcam-based object detection and video feed |
| Word-list routes | Review detected vocabulary |
| Translation routes | View translated vocabulary details |
| Handwriting routes | Practice and validate written translations |
| Gesture routes | Practice writing through hand gestures |

The exact route definitions are maintained in `voc/urls.py` and `events/urls.py`.

## Development notes

- The included `yolov5s.pt` file provides the default object-detection model used by the application.
- Camera access is required for real-time detection and gesture workflows.
- Translation services may require network access.
- SQLite, generated media, caches, and environment files are excluded from version control.
- For production deployment, configure a secure Django `SECRET_KEY`, disable `DEBUG`, set `ALLOWED_HOSTS`, and use a production database and static-file storage.

## Future improvements

- Add user accounts and personalized vocabulary progress.
- Expand language packs and offline translation support.
- Add automated tests for detection, translation, OCR, and gesture workflows.
- Replace the development SQLite setup with PostgreSQL for production.
- Add Docker and CI workflows for reproducible deployment.
- Improve model loading and inference performance for low-power devices.

## License

See the repository files for project licensing information.
