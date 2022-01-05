# useful notes

A repository for all my notes or todos. A simple script to start with and can be binded with any key. You just need a terminal emulator for this and done.

```sh 
#!/usr/bin/env bash

echo -e "Name of note:"
read -r answer
[ -z "${answer}" ] && exit
nvim "$HOME/useful-notes/${answer// /-}.md"
sleep 2s
```

Make sure the PATH exists lol

A complex variation of the script

```sh
#!/usr/bin/env bash

shopt -s lastpipe

USEFUL_NOTES="$HOME/useful-notes"
IFS=$'\n' read -r -d '' -a MARKDOWN <<< "$(find "$USEFUL_NOTES" -name "*.md")"
NOTES=( ${MARKDOWN[@]} "Create new note" )
for i in "${NOTES[@]}"; do echo "$i"; done | sort | fzf -e -i --prompt='notes: ' | read -r answer
[ -z "${answer}" ] && exit
if [ "${answer}" == "Create new note" ]
then
	command="kitty -o initial_window_width=640 -o initial_window_height=100 -o remember_window_size=no --class launcher newnotes.sh"
	setsid /bin/sh -c "${command}" >&/dev/null &
	sleep 0.3s
else
	command="kitty nvim \"${USEFUL_NOTES}/${answer}\""
	setsid /bin/sh -c "${command}" >&/dev/null &
	sleep 0.3s
fi
```

where `newnotes.sh` contains

```sh
#!/usr/bin/env bash

USEFUL_NOTES="$HOME/useful-notes"
echo -e "Name of note:"
read -r answer
[ -z "${answer}" ] && exit
command="kitty nvim \"${USEFUL_NOTES}/${answer// /-}.md\""
setsid /bin/sh -c "${command}" >&/dev/null &
sleep 0.3s
```
