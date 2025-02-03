name: Build DeepSeek Assistant

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: windows-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.8'

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Build executable
      run: |
        pip install pyinstaller
        pyinstaller --onefile --windowed --icon=assets/icon.ico main.py

    - name: Upload artifact
      uses: actions/upload-artifact@v2
      with:
        name: DeepSeek-Assistant
        path: dist/
