# MindWell Analytics — Setup and Running Guide

This guide explains how to run MindWell Analytics locally on Windows.

MindWell Analytics is an educational machine-learning project that explores relationships between students' lifestyle habits, social media usage, and a model-generated wellness score.

**Important:** This project is for educational purposes only. Its predictions are not a medical diagnosis or clinical assessment.

## 1. Prerequisites

Install the following software:

- **Python 3.10 or compatible version** supported by the project's dependencies.
- **Visual Studio Code** or another code editor.
- **Git** for version control.

Check that Python and Git are available in PowerShell:

```powershell
python --version
git --version
```

## 2. Open the project

Open PowerShell and navigate to the project folder:

```powershell
cd "$HOME\OneDrive\Desktop\Mental-Health-Score"
```

If your project is stored elsewhere, replace the path with your actual project location.

## 3. Set up the Python environment

Create a virtual environment:

```powershell
python -m venv .venv
```

Activate it:

```powershell
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, use Command Prompt or configure your PowerShell execution policy according to your organization's security guidance.

Install the required packages:

```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## 4. Start the backend

The backend uses FastAPI to validate submitted student information and generate predictions using the trained machine-learning model.

Open **Terminal 1** in the project folder. Make sure the virtual environment is activated, then run:

```powershell
uvicorn main:app --reload
```

The backend should be available at:

- API: http://127.0.0.1:8000
- Interactive API documentation: http://127.0.0.1:8000/docs

Keep this terminal open while using the application.

The backend requires `Mental_Health_Model.pkl` to be present at the location expected by `main.py`. If the application reports that the model file cannot be found, check that the file exists in the project directory.

## 5. Start the frontend

Open a **second terminal** in VS Code.

Navigate to the same project folder:

```powershell
cd "$HOME\OneDrive\Desktop\Mental-Health-Score"
```

Start the static web server:

```powershell
python -m http.server 5500
```

Open the application in your browser:

http://127.0.0.1:5500

Keep this terminal open too.

The frontend sends prediction requests to the backend at `http://127.0.0.1:8000`. Both servers must be running for predictions to work.

## 6. Test the application

1. Start the backend in Terminal 1.
2. Start the frontend in Terminal 2.
3. Open http://127.0.0.1:5500.
4. Enter the requested information in the form.
5. Submit the form.
6. Check that the predicted score appears.

You can also open http://127.0.0.1:8000/docs and test the `/predict` endpoint directly.

## 7. Troubleshooting

**Backend does not start**

- Activate `.venv`.
- Run `pip install -r requirements.txt`.
- Check that `main.py` and `Mental_Health_Model.pkl` are present where expected.

**Frontend does not open**

- Make sure the frontend server is running.
- Check that port `5500` is not already in use.
- Open the exact URL: http://127.0.0.1:5500.

**Prediction fails**

- Confirm that the backend is running at port `8000`.
- Check the browser console and backend terminal for errors.
- Confirm that the frontend's API URL points to `http://127.0.0.1:8000`.
- Check that the request values match the categories and ranges accepted by the API.

**Port already in use**

Stop the other process using the port, or choose another port and update the corresponding URL.

## 8. Stop the servers

Press `Ctrl + C` in each terminal to stop the frontend and backend servers.

## 9. Project structure

The exact structure may vary, but the main files include:

```text
Mental-Health-Score/
├── main.py
├── index.html
├── style.css
├── script.js
├── requirements.txt
├── Mental_Health_Model.pkl
├── README.md
└── RUNNING.md
```

Keep the trained model file and the frontend/backend files in the locations expected by the application.

## 10. Responsible use

This project is intended for learning and experimentation. A model-generated score should not be treated as a diagnosis, a measure of someone's worth, or a substitute for professional support.
