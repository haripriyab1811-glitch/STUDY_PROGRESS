# File and Directory Operations

Master the fundamental commands for managing files and directories in Linux.

## Basic Navigation

### `pwd` - Print Working Directory
Shows the current directory path.
```bash
pwd
# Output: /home/username/documents
```

### `cd` - Change Directory
Navigate between directories.
```bash
cd /home/username          # Absolute path
cd documents               # Relative path
cd ..                      # Go to parent directory
cd ~                       # Go to home directory
cd -                       # Go to previous directory
```

### `ls` - List Directory Contents
Display files and directories.
```bash
ls                         # Simple list
ls -l                      # Detailed list with permissions
ls -la                     # Include hidden files
ls -lh                     # Human-readable file sizes
ls -R                      # Recursive listing
ls -S                      # Sort by file size
ls -t                      # Sort by modification time
```

## Creating and Removing

### `mkdir` - Make Directory
Create new directories.
```bash
mkdir foldername           # Create single directory
mkdir -p path/to/folder    # Create nested directories
```

### `touch` - Create Empty File or Update Timestamp
```bash
touch filename.txt         # Create empty file
touch file1.txt file2.txt  # Create multiple files
```

### `rm` - Remove Files
```bash
rm filename.txt            # Remove file
rm -r directory/           # Remove directory recursively
rm -f filename.txt         # Force remove without prompt
rm -rf directory/          # Force remove directory recursively
```

### `rmdir` - Remove Empty Directory
```bash
rmdir emptyfolder          # Only works if folder is empty
```

## Copying and Moving

### `cp` - Copy Files or Directories
```bash
cp source.txt dest.txt     # Copy file
cp -r source/ dest/        # Copy directory recursively
cp -v source.txt dest.txt  # Verbose (show what's being copied)
```

### `mv` - Move or Rename Files
```bash
mv oldname.txt newname.txt # Rename file
mv file.txt /path/to/dest/ # Move file to another directory
mv source/ destination/    # Move directory
```

## Viewing File Information

### `file` - Determine File Type
```bash
file filename              # Shows file type
```

### `stat` - Display File Statistics
```bash
stat filename              # Detailed file information
```

## Practice Exercises

### Exercise 1: Basic Navigation
```bash
# 1. Print current working directory
pwd

# 2. Navigate to home directory
cd ~

# 3. List all files including hidden ones
ls -la

# 4. Return to previous directory
cd -
```

### Exercise 2: Create and Organize Folders
```bash
# 1. Create a directory structure
mkdir -p projects/python/data
mkdir -p projects/web

# 2. List the structure
ls -R projects/

# 3. Create files in different directories
touch projects/python/script.py
touch projects/web/index.html
```

### Exercise 3: Copy and Move Files
```bash
# 1. Create test files
touch file1.txt file2.txt file3.txt

# 2. Create destination directory
mkdir backup

# 3. Copy files
cp file1.txt backup/
cp file*.txt backup/

# 4. Create and move a file
touch important.txt
mv important.txt backup/important_backup.txt
```

## Common Mistakes to Avoid

❌ **Don't**: `rm -rf /` - This would delete your entire system!
✅ **Do**: Always be careful with recursive remove operations

❌ **Don't**: `rm *.txt` without checking - This deletes all text files
✅ **Do**: Use `ls *.txt` first to see what will be deleted

❌ **Don't**: Use spaces in filenames without quoting
✅ **Do**: `touch "file name.txt"` or use underscores: `touch file_name.txt`

## Quick Reference Table

| Command | Purpose | Example |
|---------|---------|---------|
| `pwd` | Print working directory | `pwd` |
| `ls` | List files | `ls -la` |
| `cd` | Change directory | `cd ~/documents` |
| `mkdir` | Create directory | `mkdir -p path/to/dir` |
| `touch` | Create file | `touch file.txt` |
| `cp` | Copy | `cp src.txt dest.txt` |
| `mv` | Move/rename | `mv old.txt new.txt` |
| `rm` | Remove | `rm -rf directory/` |
| `rmdir` | Remove empty dir | `rmdir empty/` |

---

**Next**: Read guides/02_file_viewing_searching.md
