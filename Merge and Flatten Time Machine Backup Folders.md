# MERGE TIME MACHINE FOLDERS TO A SINGLE FOLDER / DIRECTORY
**For functional Time Machine drives, you should just be able to copy the most recent backup using the Finder, which will then do all the necesary recursion for you.**

If you use recovery software to extract a Time Machine drive, you may need to flatten it down to just a single folder with all the recovered data inside. 

cd into the Root TM backups folder (or root drive if there is no root folder) 

You should have a bunch of folders That look something like below:  

/2021-9-25-12345.previous  
/2021-9-26-67890.previous  
/2021-9-29-98765.previous  
...

Then Run:
```cp -pR *.previous/ /Volumes/output/folder```

The key part is the slash after "previous", which will copy the folder contents, instead of the folder itself.
-n is no overwrites. If you use this, you'll skip over any updated copies of files that appear in later backup folders. Will speed things up though.
-p is preserve attributes
-R is include subfolders / recursion

## NOTE:
1. Found an older TM drive which didn't have ".previous" after the folder names. The process still works but used 20*/ instead to target the folder dates starting "20".
2. You may find that it takes ages copying unwanted System & Apps, so you can target within the subfolders like so: *.previous/Mac\ HDD/Users/ OR 20*/Mac\ HDD/Users/
3. Think about whether you want overwrites on or off (with the -n switch). If you use -n, the process will be faster, but you'll miss newer versions of files from later folders.
