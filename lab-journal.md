# Journal

Markdown is a method of writing information, and using syntax to format that information. This is information can be converted directly into HTML.
--- 
## Syntax
+ using "#" will create headers. Increasing the number of "#'s" will reduce the size of the header.
+ typing ** ** or __ __ will create **bold** text.
+ typing _ _ or * * will create _italicised_ text.
+ through typing "-", "+" or "*" a bullet list can be created.
+ two spaces at the end of a line will create a one line break.
+ typing "---" will create a horizontal line, useful for separating information.
+ typing "1. 2. 3. etc " will create a numbered list.
+ typing "[link]""(the actual link)" (*without the "'s*).

---

## Command-line 101
The following bullets are commands that can be entered into a terminal to achieve a certain result and an overview of what those results are.
+ "$ ls" will list the directory contents.
+ "$ cd /tmp" will move to a temporary directory (using the RAM) this will be deleted after this session, however using the RAM will mean it is a lot faster.
+ the command "cd" will change directory.
+ using the "$" sign will mean you dont have to type the entire route of the directory you are trying to reach when using the "cd" command. e.g. "cd $HOME" is the same as cd "/students/home".
+ "mkdir" will make a directory.
+ "echo "*thing*"" will write thing. " echo "Hello" > hello.md" will make a document and write "hello" in that document.
+ "cat hello.md" will write out the contents of the document "hello".
+ cp hello.md hello-again.md will create a "hello-again doc" and copy the contents of "hello" into "hello-again".
+ "mv hello-again.md hello-hello.md" will rename "hello-again" to "hello-hello".
+ "rm hello.md" will remove the doc "hello".
+ "> hi.md" will create a doc called "hi".
+ "rm -rf" will remove files without question or inhibition repeatedly.
+ "cat /proc/cpuinfo" will display the info of the cpu.

---

## Git repositories

Git repositories are for saving and sharing notes by making backup copies on the internet.  

* __git init__
  * Creates a _git_ repository by creating a hidden _.git_ folder which stores all the objects _git_ manipulates.  
* __git config user.name "Firstname Surname"__
    * Defines _user name_
* __git config user.email "email"__
    * Defines _user email_
* **git add** _file name_
    * Introduces the file _file name_ to _git_
* __git commit__ *file name*
    * Record changes to the repository/file if file name included
    * Allows us to create a message briefly explaineing about the     changes or the file.  
* __git log__
    * Displayes the history of changes in the repository.
* __>README.md__
    * It is customary to create a README file that describes using markdown syntax the content of the repository.  
* __git status__
    * This command checks if any file need to be added or if there is a change that needs to be commited.  



