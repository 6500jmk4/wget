# What is `wget`?
[GNU Wget](https://www.gnu.org/software/wget/) is a program developed by the [GNU Project](https://en.wikipedia.org/wiki/GNU_Project), which allows users to download files using the [HTTP](https://en.wikipedia.org/wiki/HTTP), [HTTPS](https://en.wikipedia.org/wiki/HTTPS), [FTP](https://en.wikipedia.org/wiki/File_Transfer_Protocol), and [FTPS](https://en.wikipedia.org/wiki/FTPS) protocols. 

The tutorial below shows you how to use Wget to download individual files and whole websites using the HTTP and HTTPS protocols. 

> [!NOTE] 
> A Note on Research Ethics
> While the `wget` command allows you to download files and websites from the internet, remember that this material has been created (and may be owned) by other people. Before you download other people's work, you should make sure that you have their permission. Some sites make their materials available freely for use (e.g. through Creative Commons licenses). For those sites for which the license is unclear, you should check with the owner. 

Wget uses a process known as [recursive retrieval](https://www.gnu.org/software/wget/manual/html_node/Recursive-Download.html). This means that it will follow the links to other directories and subdirectories and download these files as well. Its default is limited to following five links from the original file, but you can limit or expand this number as you will see in this tutorial. 

# Installing Wget

## Windows
You can download Wget by downloading the correct file file a number of sites on the internet, including https://eternallybored.org/misc/wget/. 

## Mac
Wget is not automatically installed on Mac. You will need to download it. I recommend using [Homebrew](https://brew.sh) as your package manager. 

All you need to do is navigate to the command shell where you have Homebrew installed and type
```
brew install wget
```

## Linux
If Wget is probably already installed. You can check by typing `wget` in the command line. 

If it is not already installed, all you need to do is type
```
apt-get install wget
```


# Using Wget to download individual files

If you want to download individual files from the internet, `wget` is a useful tool. All you need to do is use the command line navigate to the folder where you would like download the file. Then, you type the following into your command line:
```
wget URL 
```
You will replace URL with the url of the file you want to download. 

Type `ls` in the command line, and you will see that the file has been downloaded to your folder. 


# Using `wget` to download entire websites

For a basic download of an entire website, you would modify the command to the following:
```
wget --mirror ROOT_URL
```

The ROOT_URL is the core directory where files are stored. It is the section of the URL that ends with .org, .com. etc.

The `--mirror` argument (which can also be written as `-m`) tells `wget` to create a mirror of the site in your directory. 

A more advanced approach would be the following:
```
wget --mirror --page-requisites --convert-links ROOT_URL
```
The `--page-requisites` argument (which can also be written as `-p`)  tells `wget` to download files such as **.css** files that tell the website how it should be laid out. The reason for adding this argument is that .css files might be stored in another directory, in which case, you would lose the layout of the original website in your local copy. 

The `--convert-links` argument tells `wget` to convert internal links (e.g. links to images) so that they point to the images you have downloaded from the site rather than back to the original website. 

There are other arguments you could add as well. These include:
- `--no-clobber`: this prevents duplication and keeps the download smaller
- `--no-parent`: this tells `wget` not to grab any directories above the level in which you are working.
-  `--domains` (or `-D`): this prevents the mirror from copying pages linked outside of the domain. The argument would look like: `--domains jasonmkelly.com` or `-Djasonmkelly.com`
- `--limit-rate=##k`: this limits the speed at which you are downloading so that the demands on the external server are limited (this is good practice). The argument would look like for a rate of 100 kb/s: `--limit-rate=100k`
- `-w #`: as with `limit-rate`, this argument creates a wait time between each or your requests for files. This is important for two reasons. First, it limits pressure on the server. Second, it prevents the server from thinking that there is an attack, which could prompt it to prevent you from downloading files. The argument would look like this for a 5-second wait: `-w 5`
- `--level=#` (or `-l #`): this sets the level for recursion (i.e. how many links deep the Wget will go). The argument would look like this for a 2-level search: `-l 2`. To set it to no limit (not recommended), you would type `-l 0`  

## More Arguments

### Interrupted Downloads
If your download gets interrupted, you can try to restart where you left off with the `--continue` (or `-c`) command
```
wget -c URL
```

### Changing File Names
If you want to change the name of the file you are downloading, you would use the `--output-document` or `-O` command:
```
wget -O new_name.doc https://example.com/old_name.doc
```
This changes the original document, named **old_name.doc** to **new_name.doc**.

### Spanning Hosts
As we have already mentioned, you can limit the downloads to a specific site using `-D`. But, we can also do the opposite and request Wget to follow links outside of the file or site we are interested in looking at. 

You can use `-H` to tell Wget to download files beyond your original site. Just remember that this command can make the download much larger than you initially intended. So, it is a good idea to put a limit on the recursive search using `-l` (see above.)

### Next Steps
If you would like to learn more about Wget, you can view the user manual here: https://www.gnu.org/software/wget/manual/.
