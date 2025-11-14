# Complete Guide: Publishing Signals and Systems Course Materials to GitHub

This guide provides step-by-step instructions for publishing your Signals and Systems course materials to GitHub as a public or private repository.

## Prerequisites

1. **Git installed** on your computer
   - Download: [https://git-scm.com/downloads](https://git-scm.com/downloads)
   - Verify installation: `git --version`

2. **GitHub account**
   - Sign up: [https://github.com/signup](https://github.com/signup)

3. **GitHub Desktop (optional but recommended)**
   - Download: [https://desktop.github.com/](https://desktop.github.com/)
   - Alternative: Use command line (instructions included)

## Step-by-Step Setup

### Method 1: Using GitHub Desktop (Easier)

#### Step 1: Create Repository on GitHub

1. Go to [https://github.com/new](https://github.com/new)
2. Fill in repository details:
   - **Repository name**: `signals-and-systems-PPU`
   - **Description**: "Signals and Systems course materials - LaTeX lectures, MATLAB apps, and examples"
   - **Visibility**: Choose Public or Private
   - **DO NOT** initialize with README, .gitignore, or license (we'll add these)
3. Click **"Create repository"**

#### Step 2: Clone Repository Locally

1. Open GitHub Desktop
2. Click **"File" → "Clone Repository"**
3. Select the repository you just created
4. Choose a local path (e.g., `C:\Users\YourName\Documents\GitHub\signals-and-systems-PPU`)
5. Click **"Clone"**

#### Step 3: Organize Repository Structure

1. In the cloned repository folder, create the following structure:
   ```
   signals-and-systems-PPU/
   ├── lectures/        (your current lectures folder)
   ├── matlab-apps/     (create empty folder for now)
   └── examples/        (create empty folder for now)
   ```

2. Copy all your lecture files from `C:\Users\atoz\Desktop\Signals and Systems\lectures` to the `lectures/` folder in the cloned repository

3. Copy your MATLAB apps to the `matlab-apps/` folder

4. Copy your auxiliary examples to the `examples/` folder

#### Step 4: Move Repository Files

1. Move the following files from inside the `lectures/` folder to the root of the repository:
   - `README_ROOT.md` → rename to `README.md` (this becomes the main repo README)
   - `LICENSE` → move to root (license file)
   - `.gitignore` → move to root (git ignore rules)
   - `GITHUB_SETUP_GUIDE.md` → move to root (setup guide)

2. Keep `README_LECTURES.md` in the `lectures/` folder and rename it to `README.md` (this is specific to the lectures folder)

#### Step 5: Update .gitignore Paths

After moving `.gitignore` to the root, update the Lecture 22 exclusion paths:
1. Open `.gitignore` in a text editor
2. Change:
   ```
   lec22.tex
   figures/lec22/
   ```
3. To:
   ```
   lectures/lec22.tex
   lectures/figures/lec22/
   ```

#### Step 6: Commit and Push

1. In GitHub Desktop, you'll see all your files listed as changes
2. Write a commit message: "Initial commit: Signals and Systems course materials"
3. Click **"Commit to main"**
4. Click **"Push origin"** to upload to GitHub

### Method 2: Using Command Line (Advanced)

#### Step 1: Create Repository on GitHub

1. Go to [https://github.com/new](https://github.com/new)
2. Fill in repository details:
   - **Repository name**: `signals-and-systems-PPU`
   - **Description**: "Signals and Systems course materials - LaTeX lectures, MATLAB apps, and examples"
   - **Visibility**: Choose Public or Private
   - **DO NOT** initialize with README
3. Click **"Create repository"**

#### Step 2: Prepare Repository Structure

1. Create a new folder for your repository:
   ```powershell
   cd C:\Users\atoz\Desktop
   mkdir signals-and-systems-PPU
   cd signals-and-systems-PPU
   ```

2. Create the folder structure:
   ```powershell
   mkdir lectures
   mkdir matlab-apps
   mkdir examples
   ```

3. Copy your lectures folder content:
   ```powershell
   Copy-Item -Path "..\Signals and Systems\lectures\*" -Destination "lectures\" -Recurse
   ```

4. Move repository files to root:
   ```powershell
   Move-Item -Path "lectures\README_ROOT.md" -Destination "README.md"
   Move-Item -Path "lectures\LICENSE" -Destination "."
   Move-Item -Path "lectures\.gitignore" -Destination "."
   Move-Item -Path "lectures\GITHUB_SETUP_GUIDE.md" -Destination "."
   ```

5. Rename lectures README:
   ```powershell
   Move-Item -Path "lectures\README_LECTURES.md" -Destination "lectures\README.md"
   ```

6. Update .gitignore paths for Lecture 22 exclusion:
   - Open `.gitignore` in a text editor
   - Change:
     ```
     lec22.tex
     figures/lec22/
     ```
   - To:
     ```
     lectures/lec22.tex
     lectures/figures/lec22/
     ```

7. Copy your MATLAB apps and examples to their respective folders

#### Step 3: Initialize Git

```powershell
cd C:\Users\atoz\Desktop\signals-and-systems-PPU
git init
```

#### Step 4: Add All Files

```powershell
git add .
```

#### Step 5: Create Initial Commit

```powershell
git commit -m "Initial commit: Signals and Systems course materials"
```

#### Step 6: Connect to GitHub Repository

Replace `YOUR_USERNAME` with your actual GitHub username:

```powershell
git remote add origin https://github.com/YOUR_USERNAME/signals-and-systems-PPU.git
git branch -M main
git push -u origin main
```

You'll be prompted for your GitHub username and password (use a Personal Access Token, not your password - see authentication section below).

## GitHub Authentication

GitHub no longer accepts passwords for Git operations. You need a **Personal Access Token**:

### Creating a Personal Access Token

1. Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click **"Generate new token (classic)"**
3. Give it a name: "Signals and Systems PPU"
4. Select scopes: Check **"repo"** (full control of private repositories)
5. Click **"Generate token"**
6. **Copy the token immediately** (you won't see it again!)

### Using the Token

When Git prompts for a password, paste your Personal Access Token instead.

**For HTTPS (recommended):**
- Username: Your GitHub username
- Password: Your Personal Access Token

**Alternative: Use SSH (more secure for frequent use)**
- See: [https://docs.github.com/en/authentication/connecting-to-github-with-ssh](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)

## Repository Configuration

### Update README Files

Two README files have been created:

1. **Root README** (`README.md` in root) - Overview of the entire repository
   - Customize the **License** section if needed
   - Update **Authors** section if needed
   - Add **Contact** information if desired
   - Add descriptions for MATLAB apps and examples sections when ready

2. **Lectures README** (`lectures/README.md`) - Specific to the lecture notes
   - Already configured for the lectures folder
   - Contains compilation instructions and lecture-specific information

### Verify .gitignore

The `.gitignore` file is already configured to exclude:
- LaTeX build artifacts (`.aux`, `.log`, `.out`, etc.)
- Compiled PDFs (optional - you can remove this line if you want to track PDFs)
- Editor temporary files
- Lecture 22 files (not ready yet)

### Verify License File

A `LICENSE` file has been created with the CC BY-NC-SA 4.0 license. This file should be in the root of your repository after following the setup steps.

**To change the license (if needed):**

1. Review the `LICENSE` file and update if needed
2. If using a different Creative Commons license, visit [https://creativecommons.org/choose/](https://creativecommons.org/choose/) to generate the appropriate license text
3. Update the license section in `README.md` to match
4. For other licenses, you can use GitHub's license template:
   - Go to your repository on GitHub
   - Click **"Add file" → "Create new file"**
   - Name it `LICENSE`
   - Click **"Choose a license template"**
   - Select an appropriate license

**Important:** Verify with PPU administration that your chosen license aligns with university policies regarding faculty-created educational materials. The CC BY-NC-SA 4.0 license is recommended for educational materials but may need university approval.

## Making Updates

### Using GitHub Desktop

1. Make changes to your files
2. Open GitHub Desktop
3. Review changes in the left panel
4. Write a commit message describing your changes
5. Click **"Commit to main"**
6. Click **"Push origin"**

### Using Command Line

```powershell
cd C:\Users\atoz\Desktop\signals-and-systems-PPU
git add .
git commit -m "Description of your changes"
git push
```

## Repository Best Practices

### Commit Messages

Write clear, descriptive commit messages:
- Good: "Fix mathematical error in Lecture 11, Section 11.7.1"
- Good: "Add DFT section to Lecture 19"
- Bad: "fixes"
- Bad: "update"

### Branching (Optional)

For major changes, consider creating branches:

```powershell
git checkout -b feature/add-lecture-20
# Make changes
git commit -m "Add Lecture 20: Advanced Topics"
git push -u origin feature/add-lecture-20
```

Then create a Pull Request on GitHub to merge into main.

### Releases/Tags

Tag important versions:

```powershell
git tag -a v1.0 -m "Initial release: Complete lecture series"
git push origin v1.0
```

## Making Repository Public

If you created a private repository and want to make it public:

1. Go to your repository on GitHub
2. Click **"Settings"** tab
3. Scroll down to **"Danger Zone"**
4. Click **"Change visibility"**
5. Select **"Make public"**
6. Type the repository name to confirm

## Repository Features

### GitHub Pages (Optional)

To create a website from your repository:

1. Go to **Settings** → **Pages**
2. Under **Source**, select **"main"** branch
3. Click **"Save"**
4. Your site will be available at: `https://YOUR_USERNAME.github.io/signals-and-systems-PPU`

**Note**: This works best if you include compiled PDFs or convert to HTML.

### Issues and Discussions

Enable these features to allow:
- **Issues**: Bug reports and feature requests
- **Discussions**: Community Q&A

Go to **Settings** → **General** → **Features** to enable.

## Verifying Your Upload

After pushing, verify everything is uploaded:

1. Go to your repository on GitHub
2. Check that all folders are present:
   - `lectures/` folder with all `.tex` files
   - `matlab-apps/` folder (may be empty initially)
   - `examples/` folder (may be empty initially)
   - `README.md` in the root
   - `.gitignore` in the root
3. Click on a few files to verify content

## Troubleshooting

### "Repository not found" Error

- Verify the repository URL is correct
- Check that you have access to the repository
- Ensure you're using the correct authentication method

### "Permission denied" Error

- Verify your Personal Access Token has `repo` scope
- Check that your token hasn't expired
- Try regenerating the token

### Large File Upload Issues

If you're including PDFs or MATLAB files and they're large:
- GitHub has a 100MB file size limit
- Consider using Git LFS for large files: [https://git-lfs.github.com/](https://git-lfs.github.com/)

### Merge Conflicts

If you get merge conflicts:
1. Pull the latest changes: `git pull`
2. Resolve conflicts in the affected files
3. Commit the resolved files: `git add . && git commit -m "Resolve merge conflicts"`

## Additional Resources

- **Git Documentation**: [https://git-scm.com/doc](https://git-scm.com/doc)
- **GitHub Guides**: [https://guides.github.com/](https://guides.github.com/)
- **GitHub Desktop Guide**: [https://docs.github.com/en/desktop](https://docs.github.com/en/desktop)
- **LaTeX on GitHub**: [https://github.com/topics/latex](https://github.com/topics/latex)

## Checklist

Before publishing, ensure:

- [ ] Repository structure is correct (lectures/, matlab-apps/, examples/)
- [ ] All lecture `.tex` files are in the `lectures/` folder
- [ ] All figure files in `lectures/figures/` directory are included
- [ ] `signals-preamble.tex` is in the `lectures/` folder
- [ ] `README.md` is in the root of the repository (main repo README)
- [ ] `README.md` is in the `lectures/` folder (lectures-specific README)
- [ ] `LICENSE` is in the root of the repository
- [ ] `.gitignore` is in the root of the repository
- [ ] MATLAB apps are in `matlab-apps/` folder (if available)
- [ ] Auxiliary examples are in `examples/` folder (if available)
- [ ] No build artifacts (`.aux`, `.log`, etc.) are committed
- [ ] Lecture 22 files are excluded (not ready yet)
- [ ] Repository description is set on GitHub
- [ ] License file is in the root and properly configured

## You're Done!

Your Signals and Systems course materials are now on GitHub! Share the repository URL with students, colleagues, or the community.

**Repository URL format**: `https://github.com/YOUR_USERNAME/signals-and-systems-PPU`

---

**Need Help?** Open an issue on GitHub or consult the troubleshooting section above.
