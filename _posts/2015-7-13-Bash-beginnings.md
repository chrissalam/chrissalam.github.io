---
layout: post
title: bash beginnings
---
The Command Key (⌘) & Shortcuts and Development tools.

Starting a new profession can be overwhelming, especially when you see people dancing accross their keyboards. They are not typing faster than is possible, they've just built up an array of shortcuts and helpers that make their typing look magical. I want this magic too.

To get faster, I've begun to take serious note on typing, keyboard-based access software, text editors, and plugins within these editors, and other keyboard shortcuts that help other programmers type quickly and work faster. When starting out, new programmers are overwhelmed with the large amount of programming information they have to learn they neglect to work on the tools of coding, to explore creating items within their bash profile and using keyboard shortcuts. I would like to strongly advise against that here. **ADD A SHORTCUT KEY OR PROFILE FUNCTION TO YOUR ARSENAL DAILY.** Not only does filling your bash profile with custom functions that loop together actions you use everyday help you work faster, they help you really start to understand what your computer does and that will make you a better programmer and also help you develop a personal style of working. Here I will detail all the things I have learned to do or add to my programs to increase efficiency and have more fun while programming.

OSX and Linux based machines (POSIX based machines) have a program called terminal which if you don't have on the dock, you should consider adding. Windows uses a command prompt to do similar tasks. This program can access the internet and create and move files and folders onto your computer and run programs. I would advise learning about your particular terminal software, and if you use an extension such as ITerm2, to know how many different bash profiles you have and write your own functions and aliases, which I will go over below. These are files that are run immediately when ever you open a terminal, thus giving your permanent access to a bunch of shortcuts that can run commands to help you use github, to open local servers, and eventually run your automated tasks.

One method for getting faster is to open your bash profile and add things to it. This can be done by typing ls -a in your ~ folder and looking for { .bash_profile, .bashrc ,.mkshrc, .zshrc}. The first step is to create a method of getting into the bash profile, which can be your first function or aliases. The format for an alias is:

```bash
alias name="the command as you would otherwise type it"
```
Two must have aliases for any hopeful bash profile user are a way to open the profile and a way to reload the terminal, otherwise you would have to restart your terminal to try out changes to your bash profile. The third function I included here is a simple server I seem to use alot. I would never remember the whole sentence, thankfully I don't have to anymore.

```bash
alias prof="sublime ~/.bash_profile"
alias r=". ~/.bash_profile"
alias server="python -m SimpleHTTPServer"
```
sublime is another alias I use to open a text editor, ~/.bash_profile opens the file in the editor and I can edit and add commands. r reloads the bash profile. Explain this more.

The other main method of adding complex features to bash involve functions. Functions are generally used for broader commands and for chaining events such as opening tabs or stringing a bunch of aliases or command line tools for programs together. I'm sure you'll end up writing a bunch for yourself. The format of a function is:

```bash
functionName () {
  cd folder/of/interest
  alias1 & alias2
  doOtherPowerfulStuff
}
```
Examples of must have functionality are functions to jump around to folders you commonly use, and methods to open your common applications. I have functions that open files I need using finder, chrome, sublime, and git all in my bash profile. Shortcuts, as Hacker in Residence Josh McKeown told us early on at Telegraph Academy, take about as long to write as it takes to type out. Quit typing them out! Examples of functions I like and use are:

```bash
mkcd () {
  mkdir "$1"
  cd "$1"
}
too () {
  touch "$1"
  sublime "$1"
}
cln () {
  git clone ${1}
  cd "$1"
}
```
These commands use captures "$1" to take the text that follows the command and process it with the function. mkcd newFolder would make a new folder called newFolder, and change the directory so that you would end up within the directory upon making it. too newFile is my command for "touch and open". touch newFile makes a new file called newFile, and sublime opens it in text editor. sublime is also aliases down to the letter o elsewhere in my bash, for "opening". cln is a command that I wished I made earlier, I was constantly cloning down repos and not realizing they didn't automatically cd me into the file, and I'd start a server or open the text editor on my documents folder at first (Yikes! being a rookie...).

We were given this <a href="http://dsernst.com/2015/01/12/bring-your-own-bash-profile/">blog post as an assignment for TGA </a>, and from here I began to see a bunch of this functions but without context or explanation. I literally had not heard of bash profile at this point, roughly 3 months removed from where I am now. Later, Josh came by and gave a talk and went over a bunch of other tools and gave us this link to his github, which described showed us his bash profile and other tools such as vimium, sublime shortcuts. Here is <a href="https://github.com/joshwyatt/keyboard_shortcuts" >Josh Wyatt's very powerful suite of shortcut commands. </a>  I started with his list of bash shortcuts but commented each out until I understood exactly what they did. Many still remain in commented form, but I will get to them all and decide if I like them or will toss them. I reasoned that if I just cut and pasted them in rather than studying each individually I wouldn't learn them, so there are still of few of the ones here I've never looked at, particually git commands which I have not used yet and I've re-written other commands to fit my needs <a href="http://christophersalam.github.io/Open-with-bash/">(see this subsequent post on Jekyll Blogs and Bash).</a>

Bash profile shortcuts, coupled with learning the different ways to use your text editor, file system, and other parts of your computer are not extra features for a programmer, they are utterly required. Try to install tools to aid productivity in each piece of software you use, and try to bring all the different things you need to do into terminal or your editor. I've sped up tremendously in the last few weeks and most of that isn't do to learning frameworks or language patterns, it's because I've used shortcuts to eliminate fluffy and unesscessary typing. Thanks for reading!

------

This is a bit of a extra bit of information, don't have a full post for it yet but basically when accidently running duplicate servers, you can run this command to find the process behind the extra server and kill it 

```bash
lsof -i tcp:*8080* 
                 # or the problem port

                 # followed by 
kill -9 *processNumber*

                 # another way to
ps ax | grep node is another way to find all the node instances
```