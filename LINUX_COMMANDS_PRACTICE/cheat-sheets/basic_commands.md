# Linux Commands Quick Reference

## File & Directory Operations

```bash
pwd                     # Current directory
ls -la                  # List all files with details
cd directory            # Change directory
mkdir name              # Create directory
touch file.txt          # Create file
cp source dest          # Copy file
mv old new              # Move/rename
rm file                 # Delete file
rm -r dir               # Delete directory
```

## File Viewing

```bash
cat file.txt            # Display file contents
less file.txt           # View file page by page
head -n 10 file.txt     # First 10 lines
tail -n 10 file.txt     # Last 10 lines
wc -l file.txt          # Count lines
```

## Search & Find

```bash
grep "text" file.txt    # Search in file
grep -r "text" .        # Search recursively
find . -name "*.txt"    # Find files by name
find . -type f          # Find all files
locate filename         # Quick search (if indexed)
```

## File Permissions

```bash
chmod 755 file          # Change permissions
chmod +x script.sh      # Make executable
chown user file         # Change owner
ls -l                   # View permissions
```

## System Information

```bash
uname -a                # System information
whoami                  # Current user
df -h                   # Disk space usage
du -sh directory        # Directory size
top                     # Running processes
ps aux                  # All processes
```

## Text Processing

```bash
cat file.txt            # Display file
sed 's/old/new/' file   # Find and replace
awk '{print $1}' file   # Print column
cut -d',' -f1 file      # Cut by delimiter
sort file.txt           # Sort lines
uniq file.txt           # Remove duplicates
```

## User & Permissions

```bash
sudo command            # Run as administrator
su username             # Switch user
passwd                  # Change password
groups                  # Show user groups
id                      # User and group info
```

## Piping & Redirection

```bash
command > file          # Redirect to file
command >> file         # Append to file
command < file          # Read from file
cmd1 | cmd2             # Pipe output to next command
cmd1 && cmd2            # Run cmd2 if cmd1 succeeds
cmd1 || cmd2            # Run cmd2 if cmd1 fails
```

## Networking

```bash
ping host               # Test connectivity
ifconfig                # Network configuration
netstat -an             # Network connections
ssh user@host           # SSH connection
scp file user@host:     # Secure copy
curl url                # Fetch URL
wget url                # Download file
```

## Package Management (Ubuntu/Debian)

```bash
apt update              # Update package list
apt install package     # Install package
apt remove package      # Remove package
apt search package      # Search packages
apt upgrade             # Upgrade all packages
```

## Useful Shortcuts

```
Ctrl + C                # Stop running command
Ctrl + Z                # Suspend process
Ctrl + A                # Move to line start
Ctrl + E                # Move to line end
Ctrl + L                # Clear screen
Ctrl + R                # Search command history
!!                      # Repeat last command
!$                      # Last argument of previous command
```

---

Print this page for quick reference while practicing!
