# Linux Commands Practice Exercises

Practice exercises to build your Linux command skills. Start with Exercise 1 and progress through the levels.

## Beginner Level Exercises

### Exercise 1: Basic Navigation & Listing ⭐
**Focus**: `pwd`, `ls`, `mkdir`, `touch`, `find`

**Objectives**:
- Navigate directories using `pwd` and `cd`
- List files in different formats
- Create directory structures
- Find files by type and name

**How to Practice**:
```bash
# Make the script executable
chmod +x exercises/exercise_01_basics.sh

# Run the exercise
./exercises/exercise_01_basics.sh
```

**Manual Practice Tasks**:
```bash
# 1. Navigate and explore
pwd
cd ~
ls -la

# 2. Create a test directory
mkdir test_dir
cd test_dir

# 3. Create multiple files
touch file1.txt file2.txt file3.txt

# 4. List with different options
ls
ls -l
ls -lah
ls -S    # Sort by size
ls -t    # Sort by time

# 5. Find files
find . -type f
find . -name "*.txt"
find . -type d
```

---

### Exercise 2: File Operations
**Focus**: `cp`, `mv`, `rm`, `cat`, `wc`

**Objectives**:
- Copy files and directories
- Move and rename files
- Delete files safely
- View and count file contents

**Practice Tasks**:
```bash
# 1. Create sample files
echo "Hello World" > file1.txt
echo "Linux" > file2.txt
echo "Commands" > file3.txt

# 2. Copy files
cp file1.txt backup_file1.txt
cp *.txt backup_folder/

# 3. View content
cat file1.txt
cat file*.txt

# 4. Count lines
wc -l file1.txt
wc -w file1.txt      # Word count
wc -c file1.txt      # Byte count

# 5. Move and rename
mv file1.txt renamed_file.txt
mv renamed_file.txt backup_folder/

# 6. Safe deletion
ls *.txt             # Check before deleting
rm file2.txt
```

---

### Exercise 3: Permissions & Ownership
**Focus**: `chmod`, `chown`, `ls -l`

**Objectives**:
- Read and understand file permissions
- Change file permissions
- Change file ownership

**Practice Tasks**:
```bash
# 1. View permissions
ls -l

# 2. Understand permission format
# drwxr-xr-x = owner:rwx, group:r-x, others:r-x

# 3. Change permissions (symbolic)
chmod +x script.sh          # Make executable
chmod -r file.txt           # Remove read
chmod u+w file.txt          # Add write for user
chmod go-r file.txt         # Remove read for group and others

# 4. Change permissions (numeric)
chmod 755 script.sh         # rwxr-xr-x
chmod 644 file.txt          # rw-r--r--
chmod 700 private.txt       # rwx------

# 5. Change ownership (requires sudo)
sudo chown username file.txt
sudo chown username:groupname file.txt

# 6. Verify changes
ls -l
```

---

## Intermediate Level Exercises

### Exercise 4: Searching & Filtering
**Focus**: `grep`, `find`, `cut`, `sort`, `uniq`

**Objectives**:
- Search for text patterns
- Filter and process text
- Sort and find duplicates

**Practice Tasks**:
```bash
# 1. Create sample data
cat > data.txt << EOF
apple 5
banana 3
apple 2
orange 4
banana 1
orange 6
EOF

# 2. Search for patterns
grep "apple" data.txt
grep -n "apple" data.txt    # Show line numbers
grep -c "apple" data.txt    # Count matches
grep -i "APPLE" data.txt    # Case insensitive

# 3. Sort and unique
sort data.txt
sort -k2 data.txt           # Sort by column 2
sort -k2 -n data.txt        # Numeric sort
uniq data.txt               # Remove duplicates
sort data.txt | uniq        # Sort then unique

# 4. Cut specific fields
cut -d' ' -f1 data.txt      # First field
cut -d' ' -f2 data.txt      # Second field
```

---

### Exercise 5: Text Processing
**Focus**: `sed`, `awk`, `cut`, `tr`

**Objectives**:
- Find and replace text
- Process structured data
- Transform text

**Practice Tasks**:
```bash
# 1. Find and replace with sed
sed 's/apple/APPLE/' data.txt
sed 's/apple/APPLE/g' data.txt          # Global replace
sed -i 's/apple/APPLE/g' data.txt       # In-place edit

# 2. Delete lines with sed
sed '1d' data.txt                       # Delete line 1
sed '1,2d' data.txt                     # Delete lines 1-2
sed '/apple/d' data.txt                 # Delete lines matching pattern

# 3. Print specific lines with awk
awk '{print $1}' data.txt               # Print column 1
awk '{print $2}' data.txt               # Print column 2
awk '{print $2 + 0}' data.txt           # Numeric column

# 4. Using awk for calculation
awk '{sum += $2} END {print sum}' data.txt    # Sum column 2
awk '{print $1 ": " $2}' data.txt             # Format output
```

---

## Advanced Level Exercises

### Exercise 6: Process Management
**Focus**: `ps`, `top`, `kill`, `jobs`, `&`, `fg`, `bg`

**Objectives**:
- View running processes
- Manage foreground and background jobs
- Terminate processes

**Practice Tasks**:
```bash
# 1. View processes
ps                          # Current shell processes
ps aux                      # All processes
ps aux | grep bash          # Find specific process

# 2. View real-time processes
top                         # Press 'q' to quit
top -n 1 | head -20         # Single update, first 20 lines

# 3. Background and foreground
sleep 100 &                 # Run in background
jobs                        # Show jobs
fg                          # Bring to foreground
Ctrl + Z                    # Suspend (then use bg)
bg                          # Resume in background

# 4. Kill processes
kill PID                    # Terminate process
kill -9 PID                 # Force terminate
pkill process_name          # Kill by name
killall process_name        # Kill all instances
```

---

### Exercise 7: System Administration
**Focus**: `df`, `du`, `free`, `uname`, `hostname`, `uptime`

**Objectives**:
- Monitor system resources
- Check disk usage
- View system information

**Practice Tasks**:
```bash
# 1. Disk space
df                          # Filesystem usage
df -h                       # Human readable
df -T                       # Show filesystem type

# 2. Directory size
du -sh directory            # Total size
du -sh */                   # Size of each subdirectory
du -sh /* | sort -h         # Sorted by size

# 3. Memory usage
free                        # Memory info
free -h                     # Human readable

# 4. System information
uname -a                    # All system info
uname -r                    # Kernel release
hostname                    # System hostname
uptime                      # System uptime
who                         # Logged in users
whoami                      # Current user
```

---

### Exercise 8: Scripting Basics
**Focus**: Variables, loops, conditionals, functions

**Create File**: `script_practice.sh`
```bash
#!/bin/bash

# Variables
NAME="Linux"
VERSION="5.10"

# Simple output
echo "Learning $NAME"

# Loops
for i in {1..5}; do
    echo "Iteration $i"
done

# Conditionals
if [ -f "file.txt" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi

# Functions
greet() {
    echo "Hello, $1!"
}

greet "World"
```

**Run**:
```bash
chmod +x script_practice.sh
./script_practice.sh
```

---

## Challenge Exercises

### Challenge 1: Data Processing Pipeline
```bash
# Create a file with names and ages
cat > people.txt << EOF
Alice 25
Bob 30
Charlie 25
Diana 28
Eve 30
EOF

# Challenge: Print names of people who are 30 years old, sorted
# Solution:
awk '$2 == 30 {print $1}' people.txt | sort
```

### Challenge 2: Log File Analysis
```bash
# Create sample log
cat > app.log << EOF
2024-01-10 10:00:00 INFO User logged in
2024-01-10 10:01:00 ERROR Database connection failed
2024-01-10 10:02:00 WARNING Memory usage high
2024-01-10 10:03:00 ERROR Connection timeout
EOF

# Challenge: Count errors and warnings
# Solution:
grep "ERROR" app.log | wc -l
grep "WARNING" app.log | wc -l
```

### Challenge 3: Backup Script
```bash
# Create a script that backs up a directory with timestamp
cat > backup.sh << 'EOF'
#!/bin/bash
SOURCE="$1"
DEST="$2"
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
BACKUP_NAME="backup_$TIMESTAMP"

cp -r "$SOURCE" "$DEST/$BACKUP_NAME"
echo "Backup completed: $DEST/$BACKUP_NAME"
EOF

chmod +x backup.sh
```

---

## Progress Tracking

- [ ] Exercise 1: Navigation & Listing
- [ ] Exercise 2: File Operations
- [ ] Exercise 3: Permissions & Ownership
- [ ] Exercise 4: Searching & Filtering
- [ ] Exercise 5: Text Processing
- [ ] Exercise 6: Process Management
- [ ] Exercise 7: System Administration
- [ ] Exercise 8: Scripting Basics
- [ ] Challenge 1: Data Processing
- [ ] Challenge 2: Log Analysis
- [ ] Challenge 3: Backup Script

---

**Remember**: Practice regularly and don't be afraid to experiment!
