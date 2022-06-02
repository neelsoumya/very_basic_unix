# very_basic_unix

## Introduction

very basic UNIX commands for newbies

Very basic UNIX

1) Remove files and directories recursively within the present working directory

rm -rf *

2) Sed command to remove first line of file and save it in another file

sed '1d' test.txt > test2.txt

3) awk command to select a column from qstat and sort (to sort by name)

qstat | awk '{print $4}' | sort -k2n

k2 stands for column 2 and n is numeric ordering

 

4) Shell script to iterate through directories (from Shurane at stackoverflow)

#!/bin/bash

# Shell script to iterate through directories in pwd

for dir in */

do

        echo $dir

done

5) Shell script to iterate and cd into directories (handles directory names with spaces) (inspired by stackoverflow)

#!/bin/bash

# Shell script to iterate through directories in pwd

for dir in */

do

        echo $dir

        # go to directory

        cd "$dir"

        # run mcc to compile matlab code

        pwd

        # go back to parent directory

        cd ..

done

6) Shell script to iterate through directories (handles directories with spaces) and compiles matlab code in each of these directories

#!/bin/bash

# Shell script to iterate through directories in pwd

for dir in */

do

        echo $dir

        # go to directory

        cd "$dir"

        # run mcc to compile matlab code

        pwd

        /usr/local/MATLAB/R2011a/bin/mcc -mv unixfile.m

        # /opt/matlab/bin/mcc -mv unixfile.m

        # go back to parent directory

        cd ..

done

7) Shell script to launch multiple commands (generate "swarm" of jobs on cluster)

8) Shell script to call cellprofiler on cluster

#!/bin/sh

#S -S /bin/sh

# Shell script to call cellprofiler file

nohup /work/software/bin/cp -c -p timelapse_analysis.cp -i ~/cellprofiler_work/concatenated_and_stabilized_tifs -o ~/cellprofiler_work/cellprofiler_output_demo

# nohup /work/software/bin/cp -c -p yourpipeline_name .cp -i your_path_to_your_images -o your_output_folder_for_this_job

9) SSH login without password using ssh-keygen and ssh-copy-id (article by Ramesh Natarajan and anorther article. also see solution by DEinspanjer in an article) 

Briefly, do the following

From localhost

> ssh-keygen -t rsa -b 2048

Then

> ssh-copy-id login@remoteserver

Finally

> ssh login@remoteserver

10) Executing a sequence of commands after ssh-ing into a remote server

ssh login@remoterserver "cd codedir/matlab; ./run_script.sh; date"

Inspired by a solution by DEinspanjer in an article on copying ssh-key from a localhost that does not have ssh-copy-id to a remote server

11) Copy a directory

mkdir <new_directory_name>

cp -r <old_directory_name>/* <new_directory_name>

12) How to concatenate within shell script

echo $line >> "shell_cp$iCount.sh"

where $iCount is a variable

AND

cp $1 ${file_name_only}_${iCount}.tif

where $file_name_only and $iCount are variables

13) Store output of unix command in shell variable

present_dir=`pwd`

14) Look for substring within directory name

for dir in */

do

        echo $dir

        # cat file in directory into new file

        case $dir in

                *44*) gamma_val=44;;

                *20*) gamma_val=20;;

                *10*) gamma_val=10;;

                *) echo "this is the default case ERROR";;

        esac

       # USEFUL WORK

done

15) Shell script to copy files from all sub-directories (within the current directory) and concatenate them to create

different concatenate files (based on some substring)

for dir in */

do

        echo $dir

        # cat file in directory into new file

        case $dir in

                *44*) gamma_val=44;;

                *20*) gamma_val=20;;

                *10*) gamma_val=10;;

                *) echo "this is the default case ERROR";;

        esac

        cat "$dir"\results_jv_optimized.csv >> combined_results_jv_optimized_gamma${gamma_val}_sept252013.csv

        pwd

       

done

16) use nice command

if you cannot set priority (due to access restriction)

nice +19 program.sh

if you can set priority

nice -19 program.sh

17) Shell script to compile matlab code, wait/delay and then execute compile code

#!/bin/sh

# compile code

/usr/local/MATLAB/R2011a/bin/mcc  -mv unixfile.m

# delay: verify if compilation worked

sleep 10

# execute compiled code

nohup ./run_unixfile.sh /usr/local/MATLAB/R2011a

18) Shell script to iterate through directories in pwd and refer to file in each directory and concatenate and create a single file

#!/bin/bash

# Shell script to iterate through directories in pwd

# and refer to file in each directory and concatenate and

# and create a single file

# delete combined file if it exists

if [ -f combined_initialguess_tcl.csv ]

then

        rm  combined_initialguess_tcl.csv

else

        echo "file not found"

fi

for dir in */

do

        echo $dir

        # cat file in directory into new file

        cat "$dir"\initialguess_tcl.csv >> combined_initialguess_tcl.csv

        pwd

        # /opt/matlab/bin/mcc -mv unixfile.m

        # go back to parent directory

done

19) Shell script to copy file(s) in present directory into each sub-directory

#!/bin/bash

# Shell script to iterate through directories in pwd

# and copies some matlab files into each directory

for dir in */

do

        present_dir=`pwd`

        # copy files into each directory

        echo ${present_dir}/${dir}

        cp odecall_eclipse_tcl_jv_local_fileptr.m  "${present_dir}/${dir}"

   

done

20) Command to store output of ls command in a variable

var=`find *BFP*nuclei*`

echo "$var"

21) Command to delete swap file

# -A shows all all files

ls -A

rm -f <name_of_file>

22) Command to check if directory exists before creating a new directory

# make a temporary directory if it does not exist already

if [ ! -d agg ]

then

       mkdir agg

fi

23) Command to check if directory (using regular expression) exists before creating a new directory

# make a temporary directory if it does not exist already

if [ ! -d position_* ]

then

       mkdir agg

fi

24) Command to issue verbal alert and message by shell script on Mac OS X

say "Execution of Combined Image Analyzer successfully completed"

25) Command to check if file (regular file not directory or device file) exists

if [ -f mKate2.TIF ] && [ -f DAPI.TIF ]

then

   echo "exists"

else

   echo "does not exist"

fi

26) Unzip tgz files in Unix

tar xzvf filename.tgz

27) Unzip tar.bz2 file

tar jxf module.tar.bz2

28) Unzip tar.gz file

gunzip file.tar.gz

tar -xvf file.tar

OR

tar -zxvf file.tar.gz

# -z does gunzip

Adapted from response by Bigwebmaster at this link

29a) Unzip a gz file in Unix

gunzip filename.gz

29b) Unzip a zip file in Unix

unzip hmdb_metabolites.zip

30) Secure copy into a remote server

scp -rp   dir_name/*   user_name@remote_server:/home/dir_name

AND

# secure from remote server to localhost

scp user_name@remote_server:/home/dir_name  ./

31) Download a file(s) from a website in a shell script

wget website_url

32) watch (execute a program periodically)

watch -d ls -l

33) Extract first few lines of a file

# extract first 3 lines

head -n 3 predictions.tab > test.tab

# Select a range of lines from a file (sed, stackoverflow)

sed -n '2,50p' command_file.txt > command_file_1.txt

34) Print starting from the 3rd line of a file (using tail)

tail -n+3 test.txt

# CAUTION tail -n3 will print LAST 3 lines!

# Select a range of lines from a file (sed, stackoverflow)

sed -n '2,50p' command_file.txt > command_file_1.txt

35) Increment counter

iCount=$(( iCount+1 ))

OR

counter=`expr $counter + 1`

36) Concatenate a number to a filename (also write something to a file)

echo "#!/bin/bash" > "shell_cp$iCount.sh"

37) Cut columns 1 to 9 using cut command (default is tab delimited)

cut -f1-9 test.txt # tab delimited file

other examples see the following link

for example

cut -d':' -f3

will cut the second column from a colon (:) delimited file

# cut all columns from the 1st to the last

cut  -d ',' -f 1-   combined_hlty_prism_shotgun.csv

# cut all columns from 1st to 3rd

cut -d ',' -f -3    combined_hlty_prism_shotgun.csv

38) Do a dictionary sort on a file based on 2nd column

sort -dk2 test.tab

# numerical sort based on 2nd column

sort -nk2 test.tab

# other examples (inspired by Unix concepts and applications: Soumitabha Das)

sort -t ',' -k 2 combined_hlty_prism_shotgun.csv                # sort on 2nd field

sort -t ',' -k 1,1 -k 3,3 combined_hlty_prism_shotgun.csv   # sort on primary key 1st field and secondary key 3rd field

sort -t ',' -k 1.5,1.6 combined_hlty_prism_shotgun.csv       # sort on 6th character of 1st field (useful if mmddyy)

# removes repeated lines (unique)

sort -u

Get unique values in UNIX using uniq (link)

cat file.csv | uniq | wc -l

39) Shell script to sort on a particular column and then take that column out

#!/bin/sh

# shell script to sort compound predictions file based on column name (kegg compounds ids)

# and take out that column

# this will sort on kegg compound ids and then take out that column

# and produce a list of files of compound abundances (without the compound id columns)

# but that have been sorted on compound ids

# the output are files named temp_sorted_3.txt, etc

# then you use paste to paste together all these files like so -

# paste temp_sorted_3.txt temp_sorted_4.txt .... > combined_pasted_sorted.txt

# it also produces a file named kegg_compounds_SORTE.txt

# this has kegg compound ids and names sorted on UNIX

tail -n+2  predicted_compounds_out_3.txt | sort -dk2  | cut -f1 > kegg_compounds_SORTE.txt

iCount=1

for file_name in ls pred*.txt

do

        cat "$file_name" | sort -dk2 | cut -f2 > "temp_sorted_$iCount.txt"

        iCount=$(( iCount+1 ))

done

40) paste together files by column

paste test1.txt test2.txt

where test1.txt has

1    1

2    3

and test2.txt has

10    19

12    34

will produce

1    1    10    19

2    3    12    34

Also paste with a specified column delimiter

paste -d' ' $prev_filename $file_name > temp_file

41) copy files from one source directory to the present directory (without going to the source directory)

cp ./../normalize/module.txt module.txt

# . is current folder

## .. means go back one folder

42) sudo apt-get

and

sudo

and

 pip

For example

sudo pip install pandas

43) tr (transliterate) 

# converts ^M on Mac OS X and makes it UNIX compatible

tr '\r' '\n' < ko_ids.txt > ko_ids_modunix.txt

# using tr, convert upper case to lower case

tr '[A-Z]' '[a-z]' < combined_hlty_prism_shotgun.csv

44) join (link)

join input_json.txt input_gz.txt -1 1 -2 4 --nocheck-order -v 1

45) pr

46) curl

# simple example

curl -O http://bugs.python.org/file32324/patch_readline_issue_18458.sh

# an advanced example

curl -X POST -d '{"disease":["EFO_0000253"]}' --header 'Content-Type: application/json' https://platform-api.opentargets.io/v3/platform/public/evidence/filter\?target\=ENSG00000157764  -k > data.json

47) inverse grep

grep -v

# courtesy Galeb Abu-Ali

48) seq command (sequence)

seq --format="0_%g.dat" 0 6 60

# will print

0_0.dat

0_6.dat

0_12.dat

0_18.dat

0_24.dat

0_30.dat

0_36.dat

0_42.dat

0_48.dat

0_54.dat

0_60.dat

49) Use paste and seq together to paste together a large number of files (courtesy stackoverflow)

paste $(seq --format="temp_sorted_%g.txt" 3 355) > combined_pasted_sorted.txt

50) xargs

51) Output tab delimited file (using echo)

iCount=1

for file_name in ls pred*.txt

do

        #echo $file_name

        cat "$file_name" | tail -n+2 | sort -dk2 | cut -f2 > "temp_sorted_$iCount.txt"

        #echo "temp_sorted_$iCount.txt"

        # output mapping file

        echo "$file_name\ttemp_sorted_$iCount.txt" >> predcompounds_tempsorted.txt

        iCount=$(( iCount+1 ))

done

52) Great compilation of common UNIX commands used by a data scientist (link mazamascience.com)

53) String comparison in the shell

# Note: have to use single quotes: 'tex' and not "tex"

if [ $file_extension = 'tex' ]

then

         echo “good”

else

         echo "$0: Error, incorrect file extension (expects .tex file)"

         exit 1

fi

54) awk command to find file extension and test it

> echo test.tex | awk -F . '{print $NF}'

tex

# -F tells where to split and NF is number of fields in current line

#  Here $NF will be 2, so print $2 would print tex

# Full usage in program

file_extension=`echo $1 | awk -F . '{print $NF}' `

if [ $file_extension = 'tex' ]

then

    echo 'File extension correct'

else

    echo "$0: Error, incorrect file extension (expects .tex file)"

    exit 1

fi

55) awk command to select from a database

# From "Unix concepts and applications: Soumitabha Das"

awk -F"|"   '/sales/   { print $2, $3, $5 } '    file.txt

# selects all rows with sales and the 2nd, 3rd and 5th column

56) uniq command (inspired by Unix concepts and applications: Soumitabha Das)

# select count(*), field_name from table; group by field_name

cut -d ',' -f 1 combined_hlty_prism_shotgun.csv | sort | uniq -c

57) Find name of file only (without file extension) using basename

full_name="paper.tex"

file_extension=".tex"

basename $full_name $file_extension

> paper

58) Compare output of one command to a variable/string/number (using command substitution)

if [  ` echo $1 | awk -F . '{print $NF}'  `   =  '.tex'   ]

then

        echo 'Correct format'

else

        echo 'Incorrect format'

fi

59) Command tee (splits input into two components: one to file and another to standard output)

# display number of users

who | wc -l 

> 2

# this however does not display the users who sends output to standard output (in this case it gets piped to wc -l)

# if you want to display intermediate results on the terminal AND pipe them to another command, use tee and /dev/tty

# display users and the number of users

who | tee /dev/tty | wc -l

> user1

user2

2

# display users, display number of users and save it to file

who | tee list_users.txt | tee /dev/tty |  wc -l  >> list_users.txt

# even better

who | tee list_users.txt | tee /dev/tty |  wc -l  |  tee /dev/tty  >> list_users.txt

60) Difference between double quotes (") and single quotes (')

Double quotes allow special meta-characters like $ and ` to be evaluated by the shell

echo "The users online are `who` in $PATH"

> The users online are user1 user2 in /home/dir

# Contrast this with using single quotes

echo 'The users online are `who` in $PATH'

> The users online are `who` in $PATH

 

61) "Iterators" in shell

for temp_file_name in `ls`

do

        echo $temp_file_name

end

62) (TRICK) You want to store say file size or some other output from a command in a variable. Say

file_size=`wc -c file.txt`

echo $file_size

> 1071 file.txt

# this would also store the name of the file in $file_size

# so instead of having wc take the filename as an argument give it the filename from standard input

file_size=`wc -c < file.txt`

echo $file_size

> 1071

# now it saves just the file size in the variable $file_size

# inspired by Unix concepts and applications: Sumitabha Das (Chapter 9, The Shell)

63) Display processes with their nice value

ps -o nice

64) Rename directory

mv old_name new_name

65) ls option to ignore some files 

ls --ignore *.sh

# does not work on Mac OS X

66) Integer testing in the shell

if [ $iCount = 1 ]

then

echo “success”

else

echo “fail”

fi

67) Sleep/wait in shell

sleep 10 # sleep for 10 seconds

68) Splitting a string in shell based on a delimiter (adapted from stackoverflow) CONCEPT - parameter expansion

# Extract the 4 digit number before the underscore (_)

prev_filename=‘1003_signalp_pos’

str_partition_array=(${prev_filename//_/ })

echo ${str_partition_array[0]} # access like an array 0th element is the 4 digit number

69) Echo tab in shell script (-e option) (inspired by stackoverflow)

echo -e 'Partition_number\tDthreshold_neg\tSignalp_neg\tDthreshold_pos\tSignalp_pos\tSignalp_output_FINAL' > FINAL_parsed_file_secreted

70) elif command

        if [ $iCount = 1 ]

        then

                archaea_filename=$file_name

        elif [ $iCount = 2 ]

        then

                negative_filename=$file_name

        fi

71) A great collection of Unix commands for bioinformatics (link) (pdf)

72) View hidden files

ls -al

# can view for example .bashrc file

73) Redirect to null device

> /dev/null

74) Remove non-empty sub-directory

rm -rf <directoryname>

OR

rm -r <directoryname>

75) Command to reboot

sudo reboot

76) Universal install script (xkcd)

77) Find operating system

uname

78) temporary directory

/scratch  (no write access for user)

/tmp

/var/tmp (has write access for user)

79) grep to search for pattern in file

grep -Ein '<= SB' combined_protein_sequence.fsa.myout

see link for more grep options

80) Compress files

gzip  combined_protein_sequence.fsa

81) Tracking memory and disk usage

du -h

df  -h

82) Kill process

kill -9 <processid>

83) Path where program or application is installed

which perl

/usr/bin/perl

84) find command in UNIX (more on link)

# Find in root

find / -name call_analyze_mcmc_v122allcall4_pnpi.m -type f -print

# Find in specific directories

find /media/banerjees/SAMSUNG/ -name call_analyze_mcmc_v122allcall4_pnpi.m -type f -print

85) Select a range of lines from a file (sed, stackoverflow)

sed -n '2,50p' command_file.txt > command_file_1.txt

86) Generate ssh key and clone repo

man ssh-keygen

ssh-keygen -b 2048 -t rsa

less ~/.ssh/id_rsa.pub

git clone git@github.com:xlab/tenx.git

87) Create a symbolic link (link)

ln -s <file_path_to_simlinkto>  <new_name(optional)>

# will simlink to current directory

88) UNIX commands for bioinformatics (from link) 

grep -­‐C2 -­‐Ein 'error|exception|warning' log.txt

find . -­‐type f -­‐not -­‐name "Trinity.*" -­‐print | xargs -­‐I{} rm -­‐vfr {}

gunzip -­‐c myreads.fastq.gz | head

89) How to add a program to PATH variable

If MATLAB is installed on   ~/MATLAB/bin

then at UNIX command prompt

export PATH=$PATH:~/MATLAB/bin


90) How to append to PATH (link)


PATH=$PATH:~/soumya/local


91) Global replace in vi

:%s/foo/bar/g

to replace all instances of foo with bar globally in a document using vi
Page updated
Google Sites
Report abuse
