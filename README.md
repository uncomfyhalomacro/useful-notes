# useful notes

A repository for all my notes or todos. A simple script to start with and can be binded with any key. You just need a terminal emulator for this and done.

```sh 
#!/usr/bin/env bash

echo -e "Name of note:"
IFS=: read -r answer

nvim "$HOME/useful-notes/${answer}.md"
sleep 2s
```

Make sure the PATH exists lol
