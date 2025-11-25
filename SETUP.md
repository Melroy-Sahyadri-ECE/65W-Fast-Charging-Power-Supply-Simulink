# Setup Instructions

## Quick Setup for GitHub

### 1. Initialize Git Repository

```bash
# Navigate to your project folder
cd /path/to/your/project

# Initialize git
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit: 65W Fast Charging Power Supply Simulink Model"
```

### 2. Create GitHub Repository

1. Go to https://github.com/new
2. Repository name: `65w-fast-charging-simulink`
3. Description: `Complete Simulink model of a 65W USB-PD fast charging power supply`
4. Choose Public or Private
5. **DO NOT** initialize with README (we already have one)
6. Click "Create repository"

### 3. Push to GitHub

```bash
# Add remote (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/65w-fast-charging-simulink.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### 4. Verify Upload

Visit your repository at:
```
https://github.com/YOUR_USERNAME/65w-fast-charging-simulink
```

## Files Included

✅ `create_perfect_fast_charging.m` - Main MATLAB script  
✅ `power_supply_block_diagram.png` - Block diagram  
✅ `README.md` - Project documentation  
✅ `LICENSE` - MIT License  
✅ `.gitignore` - Git ignore rules  
✅ `CONTRIBUTING.md` - Contribution guidelines  
✅ `SETUP.md` - This file  

## Optional: Add Topics/Tags

On GitHub, add these topics to your repository:
- `matlab`
- `simulink`
- `power-electronics`
- `usb-pd`
- `fast-charging`
- `power-supply`
- `control-systems`
- `65w`

## Optional: Enable GitHub Pages

1. Go to Settings → Pages
2. Source: Deploy from branch
3. Branch: main / (root)
4. Save

Your documentation will be available at:
```
https://YOUR_USERNAME.github.io/65w-fast-charging-simulink/
```

## Need Help?

- GitHub Docs: https://docs.github.com/
- Git Basics: https://git-scm.com/book/en/v2/Getting-Started-Git-Basics

---

**That's it! Your project is now on GitHub! 🎉**
