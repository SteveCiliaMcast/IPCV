# IPCV Environment — Quick Notes (Windows)

> **Goal:** Set up a clean Python environment for your IPCV coursework and register a Jupyter kernel called **`ipcv-kernel`**.

---

## TL;DR
```powershell
# From your project folder (e.g., C:\GitHub\MCAST\IPCV\IPCV)
python -m venv ipcv

# PowerShell activation (temporary bypass if needed)
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\ipcv\Scripts\Activate.ps1

# Tools + kernel
python -m pip install --upgrade pip setuptools wheel
pip install jupyter
python -m ipykernel install --name "ipcv-kernel" --user

# Core packages
pip install numpy matplotlib imutils scikit-learn seaborn pillow opencv-contrib-python

# Done
deactivate
```

---

## 1) Create the virtual environment
From your project folder:
```powershell
python -m venv ipcv
```
> If `python` isn’t found, try `py -3 -m venv ipcv`.

This creates an isolated environment in the `ipcv` folder.

---

## 2) Activate the environment
**PowerShell (recommended):**
```powershell
# If activation is blocked by execution policy, do this first (temporary for this window only):
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass

# Then activate:
.\ipcv\Scripts\Activate.ps1
```
**Permanent user-level policy (optional):**
```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
.\ipcv\Scripts\Activate.ps1
```
**Command Prompt (no PowerShell policy involved):**
```bat
ipcv\Scriptsctivate.bat
```

> Tip: If Windows has flagged the file as downloaded-from-internet, run:
```powershell
Unblock-File .\ipcv\Scripts\Activate.ps1
```

When activated, your prompt will show `(ipcv)` at the start.

---

## 3) Install tools and register the Jupyter kernel
```powershell
python -m pip install --upgrade pip setuptools wheel
pip install jupyter
python -m ipykernel install --name "ipcv-kernel" --user
```

---

## 4) Install course packages
```powershell
pip install numpy matplotlib imutils scikit-learn seaborn pillow
pip install opencv-contrib-python
```

---

## 5) Use the kernel in VS Code / Jupyter
- Open your `.ipynb` in VS Code.
- Click the kernel picker (top-right) and select **`ipcv-kernel`**.
- New notebooks will then run inside your `ipcv` environment.

---

## 6) Verify
```powershell
python -c "import sys, cv2, numpy; print(sys.executable); print(cv2.__version__)"
pip -V
```
You should see the Python path inside `...\ipcv\Scripts\python.exe` and an OpenCV version.

---

## 7) Deactivate
```powershell
deactivate
```

---

## 8) Update later
```powershell
pip list --outdated
pip install -U <package>
# Optional: freeze for reproducibility
pip freeze > requirements.txt
```

---

## 9) Remove the kernel or environment (if ever needed)
```powershell
# Remove the Jupyter kernel
jupyter kernelspec list
jupyter kernelspec uninstall ipcv-kernel -y

# Then delete the 'ipcv' folder to remove the venv
Remove-Item -Recurse -Force .\ipcv```
> Only remove these when you’re sure you no longer need them.

---

## 10) Troubleshooting
- **Execution policy error on activation:**  
  Use the temporary bypass:
  ```powershell
  Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
  .\ipcv\Scripts\Activate.ps1
  ```
- **Multiple Python installs:**  
  Use `py -3` explicitly:
  ```powershell
  py -3 -m venv ipcv
  .\ipcv\Scripts\Activate.ps1
  ```
- **Package download issues (network/proxy):**  
  Try again or switch networks; you can also add `-i https://pypi.org/simple`.

---

**That’s it!** You now have a reproducible IPCV environment and a named Jupyter kernel ready to use.
