# GitHub setup – remaining steps

**1. Create the repo on GitHub**  
https://github.com/new → name it `BeardleysDiabloOrbsClassic` (or another name; adjust the remote URL below if so).

**2. Add the remote** (run in this addon folder):
```powershell
git remote add origin https://github.com/Serendipper/BeardleysDiabloOrbsClassic.git
```
If you used a different repo name, replace `BeardleysDiabloOrbsClassic` in the URL.

**3. First commit** (if you haven’t yet):
```powershell
git add .
git commit -m "Initial commit"
```

**4. Push and authenticate**
```powershell
git branch -M main
git push -u origin main
```
When prompted, sign in to GitHub (browser or token). Credentials are saved for this repo.

---

Already done for this project: `git init`, `credential.helper = manager`, `user.name = Serendipper`, `user.email = nova.serendipper@gmail.com`.
