# Unix Terminal Commands

I'll be honest if you're already coding, you probably know most of these. But a handbook isn't a handbook without the basics, so here we go.

---

## Working with Directories

Let's say you're dropped into a terminal and have no idea where you are or what's around you.

```bash
pwd              # prints your current location (Print Working Directory)
cd folder_name   # move into a folder
cd ..            # Change your directory (child) to parent directory 
cd ~             # go to your home directory
```

Now find what's in the current directory:

```bash
ls               # list files and folders
ls -la           # detailed list including hidden files
find . -name "main.cpp"   # search for a file by name
```

---

## Viewing Files

Once you found the file, look inside it:

```bash
cat file.txt     # print entire file content to terminal
head file.txt    # show first 10 lines
tail file.txt    # show last 10 lines
less file.txt    # scroll through file interactively (press q to quit)
```

`less` is underrated. Use it for long files instead of `cat` dumping everything at once.

---

## Searching Inside Files

```bash
grep "search_term" file.txt        # find lines containing a word
grep -r "search_term" ./folder     # search recursively through a folder
```

---

## File Operations

```bash
touch file.txt        # create an empty file
cp file.txt copy.txt  # copy a file
mv file.txt new_name.txt  # rename a file
mv file.txt ../       # move a file to parent directory
mv file.txt /folder_name # move a file to another directory
rm file.txt           # delete a file
mkdir folder_name     # create a directory
rmdir folder_name     # delete an empty directory
rm -rf folder_name    # delete a folder and everything inside it (careful)
```

---

## Permissions

This is where people get confused (At least I do). Every file in Unix has permissions for three groups: **owner**, **group**, and **everyone else**.

When you run `ls -la`, you'll see something like:

```
-rwxr-xr-- 1 user group 1234 Mar 5 12:00 script.sh
```

That first part `-rwxr-xr--` breaks down like this:

| Characters | Who | Meaning |
|---|---|---|
| `rwx` | owner | read, write, execute |
| `r-x` | group | read, no write, execute |
| `r--` | everyone | read only |

To change permissions:

```bash
chmod 755 script.sh    # rwx for owner, rx for group and everyone
chmod +x script.sh     # just add execute permission
chmod 644 file.txt     # rw for owner, r for everyone else
```

The numbers are just shorthand. Each permission has a value: read=4, write=2, execute=1. Add them up per group.

So `755` = owner gets 7 (4+2+1 = rwx), group gets 5 (4+0+1 = rx), everyone gets 5.

To change who owns a file:

```bash
chown username file.txt              # change owner
chown username:groupname file.txt    # change owner and group
```

---

## Networking

```bash
ping google.com          # check if a host is reachable
ping -c 4 google.com     # send exactly 4 packets then stop
```

`curl` is for making HTTP requests from the terminal:

```bash
curl https://api.example.com              # GET request
curl -X POST https://api.example.com \
  -H "Content-Type: application/json" \
  -d '{"key": "value"}'                  # POST request with JSON body
curl -O https://example.com/file.zip     # download a file
```

`ssh` is for connecting to remote machines:

```bash
ssh username@192.168.1.1          # connect to a server by IP
ssh username@example.com          # connect by hostname
ssh -i key.pem username@host      # connect using a private key file
```

---

## Bonus

```bash
man ls            # open the manual for any command
clear             # clean up the terminal
```
