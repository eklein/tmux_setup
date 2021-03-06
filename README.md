#NOTE

**This project is DEPRECATED and while you are welcome to use it, you may 
find these projects more interesting and updated:**

[sc_tmux](adnichols/sc_tmux) - The 'fixssh' portion of this setup moved into a gem   
[tmux-and-vim](adnichols/tmux-and-vim) - My current tmux + vim setup w/ setup script

---
Aaron Nichol's tmux setup files

CONTACT
=============================================================================
E: anichols at trumped dot org
T: @anichols

ABOUT
=============================================================================

I have put together all the various components of my tmux configuration
for someone to download and easily setup. This is covered in a blog 
post at http://www.opsbs.com/?p=261.

Most of this is intended to make remote administration over ssh easier so
if you are just looking for a tmux config, there are lots of examples out
on the Interwebs. 

These bits of code aren't works of my personal genius. They are the result
of Google searches and some experimentation with a sprinkle of fine tuning
over time. I wish i could give credit to the authors of the individual 
parts - but I have no idea who they are. 

NOTE: These tools are intended to be used under bash. If you use a different
shell and want to contribute the altered configs to work under your shell
of choice please submit a pull request w/ the additions. 

INSTALL
=============================================================================

Easy Way
-----------------------------------------------------------------------------

1. Run setup.sh from within this directory
2. Enjoy

Hard way (or, if the Easy Way doesn't work)
-----------------------------------------------------------------------------

1. Create a directory ~/bin for the scripts to live in
   (if you don't want to use this directory you don't have to
    but you will have to tweak some of the scripts to work)

`$ mkdir ~/bin`

2. Copy the contents of bin/* to your new bin directory

`$ cp -i bin/* ~/bin/`

3. Add the aliases in the 'aliases' file to a location where they 
   will get sourced upon login

One of these:

```
$ cat aliases >> ~/.bash_aliases
$ cat aliases >> ~/.bashrc
$ cat aliases >> ~/.bash_profile
```

4. Copy the tmux configuration into place (if you don't already have one)

`$ cp -i tmux.conf ~/.tmux.conf`

USAGE
=============================================================================

When you login to the host you are going to run tmux from, you will want to 
fire up tmux for the first time. The 'Attach' script by default uses
a session name of 'prod' - so you can start up your session like this:

`$ tmux -L prod`

Once that is setup, each time you login to your host you simply type:

`$ Attach`

This will connect you to your tmux session. All the sessions in an existing
tmux session will have your OLD ssh variables. To update any given session
without opening a new one type 'fixssh' which will source the fixssh file
that was created by grabssh when you ran the 'Attach' command. 

When you ssh to hosts, this is probably the hardest part to get used to, 
you need to use the 'sc' command. If you want to rename it to ssh and 
tweak your path you can, but I prefer to be able to run ssh directly too. 

To ssh to a host:

`$ sc somehostname`

This will do 3 things:
1. Fire up a new tmux window with the name set to the hostname of the host
2. Run fixssh to make sure the current ssh agent vars are set
3. ssh to the new host

That's pretty much it - if you have comments/questions shoot me an email. If 
you want to submit fixes/changes please do so via github.
