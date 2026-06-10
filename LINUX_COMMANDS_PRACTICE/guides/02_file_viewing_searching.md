# Linux File Viewing & Searching Guide

A comprehensive guide to viewing file contents and searching for files and text patterns in Linux.

## Table of Contents

1. [File Viewing Commands](#file-viewing-commands)
2. [File Searching Commands](#file-searching-commands)
3. [Text Searching Commands](#text-searching-commands)
4. [Advanced Techniques](#advanced-techniques)
5. [Common Use Cases](#common-use-cases)
6. [Practice Exercises](#practice-exercises)

---

## File Viewing Commands

### `cat` - Concatenate and Display Files

**Purpose**: Display the entire contents of one or more files.

**Basic Syntax**:
```bash
cat filename
```

**Common Options**:
```bash
cat file.txt                    # Display file contents
cat file1.txt file2.txt         # Display multiple files
cat file1.txt file2.txt > combined.txt  # Combine files
cat -n file.txt                 # Show line numbers
cat -b file.txt                 # Show line numbers (non-blank lines only)
cat -A file.txt                 # Show special characters (tabs as ^I, line ends as $)
cat -s file.txt                 # Squeeze blank lines (show only one)
```

**Example**:
```bash
$ cat document.txt
This is line 1
This is line 2
This is line 3

$ cat -n document.txt
     1	This is line 1
     2	This is line 2
     3	This is line 3
```

---

### `less` - View File Contents Page by Page

**Purpose**: View large files one page at a time (pager utility).

**Basic Syntax**:
```bash
less filename
```

**Navigation Keys**:
- `Space` or `Page Down` - Next page
- `b` or `Page Up` - Previous page
- `g` - Go to beginning
- `G` - Go to end
- `/pattern` - Search forward
- `?pattern` - Search backward
- `n` - Next search result
- `N` - Previous search result
- `q` - Quit

**Options**:
```bash
less file.txt                   # View file
less -N file.txt                # Show line numbers
less -S file.txt                # Don't wrap long lines
less +G file.txt                # Start at end of file
```

**Example**:
```bash
less large_file.txt
# Press space to scroll down
# Type /error to search for "error"
# Press q to quit
```

---

### `more` - Simple File Pager

**Purpose**: Display file contents one screen at a time (simpler than `less`).

**Basic Syntax**:
```bash
more filename
```

**Navigation Keys**:
- `Space` - Next page
- `Enter` - Next line
- `b` - Previous page
- `/pattern` - Search
- `q` - Quit

**Options**:
```bash
more file.txt
more +50 file.txt               # Start from line 50
more +/pattern file.txt         # Start from first match
```

---

### `head` - View Beginning of File

**Purpose**: Display the first few lines of a file.

**Basic Syntax**:
```bash
head [options] filename
```

**Common Options**:
```bash
head file.txt                   # First 10 lines (default)
head -n 20 file.txt             # First 20 lines
head -n 5 file.txt              # First 5 lines
head -c 100 file.txt            # First 100 characters
head -n +20 file.txt            # All lines except last 20
head -q file1.txt file2.txt     # Multiple files without headers
```

**Example**:
```bash
$ head -n 5 document.txt
Line 1
Line 2
Line 3
Line 4
Line 5
```

---

### `tail` - View End of File

**Purpose**: Display the last few lines of a file.

**Basic Syntax**:
```bash
tail [options] filename
```

**Common Options**:
```bash
tail file.txt                   # Last 10 lines (default)
tail -n 20 file.txt             # Last 20 lines
tail -n +5 file.txt             # From line 5 to end
tail -c 100 file.txt            # Last 100 characters
tail -f file.txt                # Follow file (useful for logs)
tail -F file.txt                # Follow file (retry if rotated)
tail --pid=PID -f file.txt      # Stop following when process ends
```

**Example**:
```bash
$ tail -n 5 document.txt
Line 11
Line 12
Line 13
Line 14
Line 15

$ tail -f log.txt
# Continuously shows new lines as they appear
```

**Real-time Log Monitoring**:
```bash
tail -f /var/log/syslog         # Monitor system log
tail -f /var/log/apache2/access.log  # Monitor web server
```

---

### `wc` - Word/Line/Character Count

**Purpose**: Count lines, words, and characters in files.

**Basic Syntax**:
```bash
wc [options] filename
```

**Common Options**:
```bash
wc file.txt                     # Lines, words, and bytes
wc -l file.txt                  # Line count only
wc -w file.txt                  # Word count only
wc -c file.txt                  # Byte count only
wc -m file.txt                  # Character count
wc -L file.txt                  # Longest line length
wc -l *.txt                     # Count lines in all .txt files
wc -l *.txt | tail -1           # Total lines in all files
```

**Example**:
```bash
$ wc document.txt
 15  45 342 document.txt
# 15 lines, 45 words, 342 bytes

$ wc -l document.txt
15 document.txt
```

---

### `file` - Determine File Type

**Purpose**: Display the type and properties of a file.

**Basic Syntax**:
```bash
file filename
```

**Options**:
```bash
file document.txt               # Show file type
file -b document.txt            # Brief output (no filename)
file -i document.txt            # MIME type
file *.txt                      # Multiple files
file /path/to/file              # Full path
```

**Example**:
```bash
$ file document.txt
document.txt: ASCII text

$ file image.png
image.png: PNG image data, 1920 x 1080, 8-bit/color RGBA, non-interlaced

$ file script.sh
script.sh: Bourne-Again shell script text executable, ASCII text
```

---

## File Searching Commands

### `find` - Search for Files

**Purpose**: Recursively search for files based on various criteria.

**Basic Syntax**:
```bash
find path criteria action
```

**Common Criteria**:
```bash
# By name
find . -name "file.txt"         # Exact filename
find . -name "*.txt"            # Wildcard pattern
find . -name "*.txt" -o -name "*.md"  # Multiple patterns (OR)
find . -iname "FILE.TXT"        # Case-insensitive

# By type
find . -type f                  # Regular files only
find . -type d                  # Directories only
find . -type l                  # Symbolic links
find . -type s                  # Sockets
find . -type p                  # Named pipes

# By size
find . -size +1G                # Larger than 1GB
find . -size -10M               # Smaller than 10MB
find . -size 100k               # Exactly 100KB

# By time
find . -mtime -7                # Modified in last 7 days
find . -mtime +30               # Modified more than 30 days ago
find . -atime -1                # Accessed in last day
find . -ctime 0                 # Changed today

# By permissions
find . -perm 755                # Exact permissions
find . -perm -u+x               # Executable by user
find . -perm /a+x               # Executable by anyone

# By ownership
find . -user username           # Owned by user
find . -group groupname         # Owned by group
```

**Actions**:
```bash
find . -name "*.txt" -print     # Print results (default)
find . -name "*.txt" -delete    # Delete matching files
find . -name "*.tmp" -delete    # Delete temp files
find . -type f -exec chmod 644 {} \;  # Execute command on each
find . -name "*.log" -exec ls -l {} \;  # List details
```

**Complex Examples**:
```bash
# Find all .txt files larger than 1MB modified in last week
find . -type f -name "*.txt" -size +1M -mtime -7

# Find empty directories
find . -type d -empty

# Find and delete files older than 30 days
find . -type f -mtime +30 -delete

# Find .js files (excluding node_modules)
find . -name node_modules -prune -o -name "*.js" -print

# Find all files modified in last hour and show details
find . -type f -mmin -60 -exec ls -lh {} \;
```

---

### `locate` - Find Files by Name (Database)

**Purpose**: Quickly search for files using a pre-built database.

**Basic Syntax**:
```bash
locate filename
```

**Options**:
```bash
locate file.txt                 # Find files with this name
locate -i FILE.TXT              # Case-insensitive search
locate -c "*.txt"               # Count matches
locate -r ".*\.txt$"            # Regex pattern
locate --regex "pattern"        # Extended regex
```

**Update Database**:
```bash
sudo updatedb                   # Update locate database
```

**Example**:
```bash
$ locate document.txt
/home/user/documents/document.txt
/home/user/backup/document.txt

# Much faster than find for large directory trees
```

---

### `which` - Locate Command Programs

**Purpose**: Find the location of executable files in PATH.

**Basic Syntax**:
```bash
which command
```

**Options**:
```bash
which python                    # Find python executable
which -a python                 # All occurrences
which ls                        # Find ls command
```

**Example**:
```bash
$ which python
/usr/bin/python

$ which -a python
/usr/bin/python
/usr/local/bin/python
```

---

### `whereis` - Locate Command Source, Binary, Manual

**Purpose**: Find binary, source, and manual page locations.

**Basic Syntax**:
```bash
whereis command
```

**Options**:
```bash
whereis python                  # Find python files
whereis -b python               # Binary only
whereis -s python               # Source only
whereis -m python               # Manual page only
```

**Example**:
```bash
$ whereis python
python: /usr/bin/python /usr/lib/python3.9 /usr/share/man/man1/python.1.gz
```

---

## Text Searching Commands

### `grep` - Search Text Patterns

**Purpose**: Search for lines matching a pattern in files.

**Basic Syntax**:
```bash
grep pattern filename
grep pattern *.txt              # Multiple files
```

**Common Options**:
```bash
grep "error" log.txt            # Basic search
grep -i "ERROR" log.txt         # Case-insensitive
grep -c "error" log.txt         # Count matching lines
grep -n "error" log.txt         # Show line numbers
grep -v "error" log.txt         # Invert match (exclude)
grep -l "error" *.txt           # List files with matches
grep -r "error" .               # Recursive search
grep -w "word" file.txt         # Whole word match
grep -E "pattern|pattern2" file.txt  # Extended regex (OR)
grep -F "literal.string" file.txt    # Literal string (no regex)
```

**Advanced Options**:
```bash
grep -B 3 "error" log.txt       # 3 lines before match
grep -A 3 "error" log.txt       # 3 lines after match
grep -C 3 "error" log.txt       # 3 lines before and after
grep -m 5 "pattern" file.txt    # Stop after 5 matches
grep -e "pat1" -e "pat2" file   # Multiple patterns (OR)
```

**Examples**:
```bash
# Find all ERROR lines in log file
grep "ERROR" app.log

# Find lines without "DEBUG"
grep -v "DEBUG" app.log

# Find "Connection" in all .log files with line numbers
grep -n "Connection" *.log

# Find whole word "server" (not "servers")
grep -w "server" config.txt

# Search recursively in all directories
grep -r "TODO" .

# Case-insensitive search with 2 lines context
grep -i -C 2 "warning" syslog

# Find lines starting with "Error:"
grep "^Error:" log.txt

# Find lines ending with numbers
grep "[0-9]$" data.txt
```

---

### `egrep` / `grep -E` - Extended Regular Expressions

**Purpose**: Use extended regex patterns for complex searches.

**Basic Syntax**:
```bash
grep -E "pattern" file
egrep "pattern" file            # Same as above
```

**Examples**:
```bash
# Multiple patterns (OR)
grep -E "error|warning|fatal" log.txt

# Email pattern
grep -E "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$" emails.txt

# IP addresses
grep -E "^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}$" ips.txt

# Word boundaries
grep -E "\btest\b" document.txt
```

---

### `fgrep` / `grep -F` - Fixed String Search

**Purpose**: Search for literal strings (no regex interpretation).

**Basic Syntax**:
```bash
grep -F "literal.string" file
fgrep "literal.string" file     # Same as above
```

**Useful For**:
```bash
# Search for strings with special characters
grep -F "C++" source.txt

# Search for regex patterns as literal text
grep -F "^error" log.txt        # Finds actual "^error" text
```

---

### `zgrep` - Search Compressed Files

**Purpose**: Search within gzip-compressed files.

**Basic Syntax**:
```bash
zgrep pattern file.gz
```

**Example**:
```bash
zgrep "error" compressed.log.gz
zgrep -c "ERROR" app.log.gz
```

---

## Advanced Techniques

### Combining Commands with Pipes

```bash
# Find all .txt files and count them
find . -name "*.txt" | wc -l

# Search in large files efficiently
cat huge_file.txt | grep "pattern" | head -20

# Combine grep and awk for processing
grep "ERROR" log.txt | awk '{print $3}' | sort | uniq -c

# Filter files before searching
find . -name "*.log" | xargs grep "warning"
```

---

### Search and Replace with `sed`

**Basic Syntax**:
```bash
sed 's/old/new/' file.txt       # Replace first occurrence per line
sed 's/old/new/g' file.txt      # Replace all occurrences
sed -i 's/old/new/g' file.txt   # In-place edit (backup: -i.bak)
```

**Examples**:
```bash
# Find and display matches
sed -n '/pattern/p' file.txt

# Delete lines matching pattern
sed '/pattern/d' file.txt

# Case-insensitive replacement
sed 's/ERROR/FATAL/gi' log.txt
```

---

### Using `awk` for Advanced Searching

**Basic Syntax**:
```bash
awk '/pattern/ {action}' file
```

**Examples**:
```bash
# Print lines matching pattern
awk '/error/ {print}' log.txt

# Print specific columns for matching lines
awk '/ERROR/ {print $1, $3}' log.txt

# Count matching lines
awk '/error/ {count++} END {print count}' log.txt

# Print lines where column 2 > 100
awk '$2 > 100 {print}' data.txt
```

---

## Common Use Cases

### 1. Finding Large Files

```bash
# Files larger than 100MB
find . -type f -size +100M

# Show sizes
find . -type f -size +100M -exec ls -lh {} \; | awk '{print $9, $5}'

# Or using du
du -sh */ | sort -hr | head -10
```

---

### 2. Monitoring Log Files

```bash
# View last 20 lines of log
tail -n 20 /var/log/syslog

# Follow log in real-time
tail -f /var/log/syslog

# Count errors in log
grep -c "ERROR" app.log

# Show errors with context
grep -B2 -A2 "ERROR" app.log
```

---

### 3. Finding Files Modified Recently

```bash
# Files modified in last 24 hours
find . -type f -mtime -1

# Files modified in last 1 hour
find . -type f -mmin -60

# Show details
find . -type f -mmin -60 -exec ls -lh {} \;
```

---

### 4. Searching Code

```bash
# Find Python files with specific function
grep -r "def function_name" --include="*.py" .

# Find TODO comments in code
grep -rn "TODO" --include="*.js" .

# Case-insensitive search in Java files
grep -ri "classname" --include="*.java" .
```

---

### 5. Recursive Search and Replace

```bash
# Find and replace in all .txt files
find . -name "*.txt" -exec sed -i 's/old/new/g' {} \;

# More efficiently using xargs
find . -name "*.txt" -print0 | xargs -0 sed -i 's/old/new/g'

# With backup
find . -name "*.txt" -exec sed -i.bak 's/old/new/g' {} \;
```

---

## Practice Exercises

### Exercise 1: Basic File Viewing

```bash
# 1. Create a sample file
cat > sample.txt << EOF
Line 1: First line
Line 2: Second line
Line 3: Third line
Line 4: Fourth line
Line 5: Fifth line
EOF

# 2. View entire file
cat sample.txt

# 3. View with line numbers
cat -n sample.txt

# 4. View first 3 lines
head -n 3 sample.txt

# 5. View last 2 lines
tail -n 2 sample.txt

# 6. Count lines
wc -l sample.txt
```

---

### Exercise 2: Searching and Filtering

```bash
# 1. Create a data file
cat > data.txt << EOF
apple 100 red
banana 80 yellow
cherry 50 red
date 200 brown
elderberry 30 purple
fig 150 brown
EOF

# 2. Find lines containing "red"
grep "red" data.txt

# 3. Find lines NOT containing "red"
grep -v "red" data.txt

# 4. Show line numbers
grep -n "red" data.txt

# 5. Case-insensitive search
grep -i "APPLE" data.txt

# 6. Count matching lines
grep -c "red" data.txt
```

---

### Exercise 3: Advanced Searching

```bash
# 1. Find all .md files in current directory
find . -name "*.md" -type f

# 2. Find files modified in last 7 days
find . -type f -mtime -7

# 3. Find directories only
find . -type d

# 4. Find executable files
find . -type f -executable

# 5. Search for pattern in all .txt files
grep -r "pattern" --include="*.txt" .

# 6. Find and display details
find . -name "*.log" -exec ls -lh {} \;
```

---

### Exercise 4: Text Processing Pipeline

```bash
# 1. Create a log file
cat > app.log << EOF
2024-01-10 10:00:00 INFO User login
2024-01-10 10:01:00 ERROR Database connection failed
2024-01-10 10:02:00 WARNING Memory usage 85%
2024-01-10 10:03:00 INFO User logout
2024-01-10 10:04:00 ERROR Timeout occurred
EOF

# 2. Find all errors
grep "ERROR" app.log

# 3. Count errors
grep "ERROR" app.log | wc -l

# 4. Show errors with timestamps
grep "ERROR" app.log | awk '{print $1, $2, $NF}'

# 5. Find ERROR or WARNING
grep -E "ERROR|WARNING" app.log

# 6. Count each type
grep "ERROR" app.log | wc -l
grep "WARNING" app.log | wc -l
grep "INFO" app.log | wc -l
```

---

## Quick Reference Table

| Command | Purpose | Example |
|---------|---------|---------|
| `cat` | Display file contents | `cat file.txt` |
| `less` | Page through file | `less large.txt` |
| `head` | First N lines | `head -n 20 file.txt` |
| `tail` | Last N lines | `tail -n 10 file.txt` |
| `wc` | Count lines/words/bytes | `wc -l file.txt` |
| `find` | Search for files | `find . -name "*.txt"` |
| `locate` | Quick file search | `locate file.txt` |
| `grep` | Search text patterns | `grep "error" log.txt` |
| `sed` | Find and replace | `sed 's/old/new/g' file.txt` |
| `awk` | Text processing | `awk '{print $1}' file.txt` |

---

**Remember**: Master these commands and you'll be able to efficiently navigate, view, and search files in Linux!
