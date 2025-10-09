# IPCV Environment — Quick Notes (macOS, Apple Silicon)

## What we set up
- Installed **Python 3** so `python3`/`pip3` are available.
- Created a **virtual environment** named `ipcv` inside your `IPCV` folder.
- Installed Jupyter + core libraries (NumPy, Matplotlib, scikit-learn, etc.).
- Registered a **Jupyter kernel** called **Python (ipcv)** so notebooks can use this env in VS Code.

> Tip: On macOS, always prefer `python3` or `python -m pip`.

---

## Create the environment (one time)
From the **VS Code terminal** inside your `IPCV` folder:
```bash
python3 -m venv ipcv
source ipcv/bin/activate
python -m pip install --upgrade pip setuptools wheel
python -m pip install jupyter ipykernel
python -m pip install numpy matplotlib imutils scikit-learn seaborn pillow
python -m pip install opencv-contrib-python   # if this fails, try: python -m pip install opencv-python
python -m ipykernel install --user --name=ipcv --display-name "Python (ipcv)"
```

Packages installed:
- `jupyter`, `ipykernel`
- `numpy`, `matplotlib`, `imutils`, `scikit-learn`, `seaborn`, `pillow`
- `opencv-contrib-python` (or `opencv-python` as fallback)

---

## Activate & use the env (every time you work)
1. Open VS Code in your `IPCV` folder.
2. **Activate the env in the terminal:**
   ```bash
   source ipcv/bin/activate
   ```
   You’ll see your prompt change to `(ipcv)`.
3. In the notebook toolbar, set the kernel to **Python (ipcv)** (or use the bottom-right kernel picker in VS Code).

---

## Deactivate the env (when you’re done)
```bash
deactivate
```

---

## Common checks
```bash
python --version         # inside the env, this should report Python 3.x
python -m pip --version  # confirms pip belongs to the active env
jupyter --version        # confirms Jupyter is installed in the env
```

---

## If Python isn’t found yet (one-time install)
**Homebrew (recommended):**
```bash
# Install Homebrew if needed:
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

# Then Python:
brew install python@3.12
```
Now retry the steps above.
