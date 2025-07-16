# DayZ Server Files - Git Commands Reference

This document contains the commands and processes used to successfully push DayZ server configuration files to GitHub.

## Repository Information

- **GitHub Repository**: https://github.com/DUCKMAN2016/DayZ-Stuff.git
- **User**: DUCKMAN2016
- **Email**: duckman2016@gmail.com

## What Was Pushed

The following DayZ server configuration files were successfully pushed to GitHub:

1. **Chernarus Map Files**
   - Server configuration (.cfg files)
   - Mission configuration files (XML and JSON)
   - Mod configuration files
   - Text configuration (.txt files)

2. **DeerIsle Map Files**
   - Server configuration (.cfg files)
   - Mission configuration files (XML and JSON)
   - Text configuration (.txt files)
   
3. **Fallujah Map Files**
   - Server configuration (.cfg files)
   - Mission configuration files (XML and JSON)
   - Text configuration (.txt files)

4. **FrosLine Map Files**
   - Server configuration (.cfg files)
   - Mission configuration files (XML and JSON)
   - Text configuration (.txt files)

5. **Namalsk Map Files**
   - Server configuration (.cfg files)
   - Mission configuration files (XML and JSON)
   - Environment territory files
   - Text configuration (.txt files)
   
6. **NewYork Map Files**
   - Server configuration (.cfg files)
   - Mission configuration files (XML and JSON)
   - Text configuration (.txt files)

7. **Additional Files**
   - `.gitignore` to exclude large binary files
   - `README.md` with repository information

**Note**: Large binary files (.bin, .map, .db) and database backup files were excluded to keep the repository manageable.

## Git Commands Used

### Setting Up a New Repository

```bash
# Initial setup
mkdir -p /path/to/repo
cd /path/to/repo
git init
git config --local user.name "DUCKMAN2016"
git config --local user.email "duckman2016@gmail.com"

# Create initial README
echo "# DayZ Server Files" > README.md
git add README.md
git commit -m "Initial commit"

# Add remote repository
git remote add origin https://github.com/DUCKMAN2016/DayZ-Stuff.git

# Push initial commit
git push -u origin main
```

### Pushing Configuration Files Only

```bash
# Clone repository to clean directory
git clone https://github.com/DUCKMAN2016/DayZ-Stuff.git /path/to/clean/dir
cd /path/to/clean/dir

# Create .gitignore for binary files
cat > .gitignore << EOF
# Ignore large binary files and databases
*.bin
*.map
*.db
*.001
*.002
*.lock
storage_*/data/
storage_*/backup/
EOF

# Copy only configuration files
# (Use find with proper path handling to maintain directory structure)
find /source/dir -name "*.cfg" -exec cp --parents {} /path/to/clean/dir \;
find /source/dir -name "*.xml" -exec cp --parents {} /path/to/clean/dir \;
find /source/dir -name "*.json" -exec cp --parents {} /path/to/clean/dir \;
find /source/dir -name "*.txt" -exec cp --parents {} /path/to/clean/dir \;

# Add all files
git add -v .

# Commit changes
git commit -v -m "Update DayZ server configuration files"

# Push changes
git push -v origin main
```

### Fixing Directory Structure Issues

If full paths are accidentally committed, use these commands to fix:

```bash
# Clone repository
git clone https://github.com/DUCKMAN2016/DayZ-Stuff.git /path/to/fix/dir
cd /path/to/fix/dir

# Remove unwanted directories
git rm -r path/to/unwanted/directory

# Commit changes
git commit -v -m "Remove incorrectly named directory with full path"

# Push changes
git push -v origin main
```

### Handling Conflicts with Remote Changes

```bash
# Pull with rebase to handle conflicts
git pull --rebase -v origin main

# Push after resolving conflicts
git push -v origin main
```

## Best Practices for Future Updates

1. **Always use verbose output** with `-v` flag for Git commands to monitor progress
2. **Use .gitignore** to exclude large binary files and database backups
3. **Clone to a fresh directory** before making major changes
4. **Check directory structure** before pushing to avoid path issues
5. **Use `--force` with caution** only when necessary to restructure the repository
6. **Break up large commits** if pushing more than 100MB of data

## Automation Scripts Created

1. `push_config_fixed.sh` - Script to push only configuration files with proper directory structure
2. `remove_unwanted_dir.sh` - Script to remove incorrectly added full paths

## Troubleshooting Common Issues

1. **Push rejected errors**: Use `git pull --rebase origin main` before pushing
2. **File too large errors**: Add large files to .gitignore or use Git LFS
3. **Timeout errors**: Break up commits into smaller chunks
4. **Path structure issues**: Use proper path handling in scripts when copying files
