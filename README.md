# docs
Useful command line tools with the relevant switches I use for certain jobs. Mostly Macs, but maybe some other Unix / Linux stuff.  

```cp -R /var/www /new/folder ```  
Avoid the extra forward slash at the end of the path name.  
If you add a slash to the end of the source directory, it will copy the contents from the folder  
  
To copy a whole Mac Disk Use:  
```sudo cp -pR /Volumes/Macintosh\ HD/ /Volumes/NewDisk```  

Note the slash after HD, which you'll need to add if you drop the volume into the terminal window. If you don't add the slash, you'll end up with a Macintosh HD folder inside NewDisk. There is no slash after NewDisk.

Or

you can navigate to the /var directory in terminal and then try

cp -pR www /new/folder

-p flag preserves dates & times from original files.

add the -n flag to prevent overwriting files. Handy for filling in missing data from a previous copy, or if the process gets interrupted. Example below: 

sudo cp -npR /Volumes/Macintosh\ HD/ /Volumes/NewDisk

For progress information on Mac, try "ctrl + t" to send SIGINFO command during the copy.


EXAMPLE

If the www folder contains index.html

$>cp -R /var/www /new/folder 
will make /new/folder/www/index.html

With a slash on the source folder
$>cp -R /var/www/ /new/folder
Will make /new/folder/index.html

***************************************************

FIX MAC GREYED OUT FINDER FILES FOLDERS BAD DATES

SetFile -d '12/31/1999 23:59:59' /Volumes/Folder/Goes/Here

This changes the creation date from a faulty one (like 1984) to a real one.

***************************************************
NEW MAC ONE TO TRY:
ditto /folder/folder1 /folder/folder2

This is designed to work by just dropping the source & destination folders onto terminal. No need to add slashes etc.

***************************************************
MERGE TIME MACHINE FOLDERS TO A SINGLE FOLDER DIRECTORY

If you extract a Time Machine drive, and need to flatten it down to just a single folder with all the recovered data, try the below (from 212857)

cd into the Root folder (or root drive if there is no root folder) 

You should have a bunch of folders with 

/Root
	/2021-9-25-12345.previous
	/2021-9-26-67890.previous
	/2021-9-29-98765.previous

Then Run:
cp -npR *.previous/ /Volumes/output/folder

The key part is the slash after "previous", which will copy the folder contents, instead of the folder itself.
-n is no overwrites
-p is preserve attributes
-R is include subfolders / recursion

NOTE:
Found an older TM drive which didn't have ".previous" after the folder names. The process still works but used 20*/ instead to target the folder dates starting "20".

You may find that it takes ages copying unwanted System & Apps, so you can target within the subfolders like so: *.previous/Mac\ HDD/Users/ OR 20*/Mac\ HDD/Users/

Think about whether you want overwrites on or off (with the -n switch). If you use -n, the process will be faster, but you'll miss newer versions of files from later folders.

***************************************************

Windows XCOPY:

xcopy "C:\Important Files" D:\Backup /c /d /e /h /i /k /q /r /s /x /y

Life's too short to explain all those switches :-/


TIDY MAC FILE LISTS:  
```ls -hR [drag folder here] > JOBNUMBER.txt```

FIND EMPTY OR BLANK FILES IN LINUX  
```find ~/list \( -empty -o \( -type f -a ! -exec grep -qm1 '[^[:blank:]]' {} \; \) \) -exec ls -Fd {} \;```

CAN ALSO BE PIPED TO A LIST:
find ~/list \( -empty -o \( -type f -a ! -exec grep -qm1 '[^[:blank:]]' {} \; \) \) -exec ls -Fd {} \; >ZEROFILES.txt

IF YOU'RE CAREFUL YOU CAN THEN DELETE THE LISTED FILES:
while IFS= read -r file ; do rm -- "$file" ; done < ZEROFILES.txt

Check the list first, as anything odd could cause dangerous results!
I removed the * from after each line by doing a find & replace on the list before deleting the files.

GREP FOR TEXT AND SHOW LINES BEFORE AND AFTER
For BSD or GNU grep you can use -B num to set how many lines before the match and -A num for the number of lines after the match.

grep -B 3 -A 2 foo README.txt
If you want the same number of lines before and after you can use -C num.

grep -C 3 foo README.txt
This will show 3 lines before and 3 lines after.

***************************************************
That annoying thing where Mac won't eject an external disk. (It's usually spotlight)  
```lsof /Volumes/USB```  
or  
```sudo lsof /Volumes/USB```  
