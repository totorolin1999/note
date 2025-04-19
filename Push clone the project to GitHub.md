# Push/clone the project to GitHub

# Push

---

### If it is a Django project.

```powershell
python -m venv venv
venv\Scripts\activate
# deactivate
# rm -r venv
```

```powershell
pip freeze
pip freeze --local
pip freeze --local > requirements.txt
```

---

### First Time

```powershell
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin 網址
git push -u origin main
```

### Second Time

```powershell
git add .
git commit -m "second commit"
git push
```

---

# Clone

---

```powershell
git clone 網址
```

---

### If it is a Django project.

```powershell
python -m venv venv
venv\Scripts\activate
# deactivate
# rm -r venv
```

```powershell
pip install -r requirements.txt
```

---

### If it is a React project.

```powershell
npm install
# yarn install
```

# References

[【git教學 #1】15分鐘學會git & github（附實例）](https://www.youtube.com/watch?v=Zd5jSDRjWfA)

[Create and clone a new repository on GitHub](https://www.youtube.com/watch?v=Oz8rtnBJHlA)

[Virtual Environments in Python - Crash Course](https://www.youtube.com/watch?v=IAvAlS0CuxI)

[Python venv: How To Create, Activate, Deactivate, And Delete](https://python.land/virtual-environments/virtualenv)

[How To Create A Django Project - Installation, Setup And Virtual Environment](https://www.youtube.com/watch?v=HBE4K1Xu9us)