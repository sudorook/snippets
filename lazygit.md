# lazygit Keymap

## Global Keybindings

[Reference](https://github.com/jesseduffield/lazygit/blob/master/docs/keybindings/Keybindings_en.md)

| Key    | Description                                                            |
| ------ | ---------------------------------------------------------------------- |
| ctrl+r | switch to a recent repo                                                |
| pgup   | scroll up main panel (fn+up/shift+k)                                   |
| pgdown | scroll down main panel (fn+down/shift+j)                               |
| @      | open command log menu                                                  |
| }      | Increase the size of the context shown around changes in the diff view |
| {      | Decrease the size of the context shown around changes in the diff view |
| :      | execute custom command                                                 |
| ctrl+p | view custom patch options                                              |
| m      | view merge/rebase options                                              |
| R      | refresh                                                                |
| +      | next screen mode (normal/half/fullscreen)                              |
| \_     | prev screen mode                                                       |
| ?      | open menu                                                              |
| ctrl+s | view filter-by-path options                                            |
| W      | open diff menu                                                         |
| ctrl+e | open diff menu                                                         |
| ctrl+w | Toggle whether or not whitespace changes are shown in the diff view    |
| z      | undo (via reflog) (experimental)                                       |
| ctrl+z | redo (via reflog) (experimental)                                       |
| P      | push                                                                   |
| p      | pull                                                                   |

## List Panel Navigation

| Key | Description      |
| --- | ---------------- |
| ,   | previous page    |
| .   | next page        |
| <   | scroll to top    |
| /   | start search     |
| >   | scroll to bottom |
| H   | scroll left      |
| L   | scroll right     |
| ]   | next tab         |
| [   | previous tab     |

## Commit Files

| Key    | Description                                                                   |
| ------ | ----------------------------------------------------------------------------- |
| ctrl+o | copy the committed file name to the clipboard                                 |
| c      | checkout file                                                                 |
| d      | discard this commit's changes to this file                                    |
| o      | open file                                                                     |
| e      | edit file                                                                     |
| space  | toggle file included in patch                                                 |
| a      | toggle all files included in patch                                            |
| enter  | enter file to add selected lines to the patch (or toggle directory collapsed) |
| `      | toggle file tree view                                                         |

## Commit Summary

| Key   | Description |
| ----- | ----------- |
| enter | confirm     |
| esc   | close       |

## Commits

| Key    | Description                                                    |
| ------ | -------------------------------------------------------------- |
| ctrl+o | copy commit SHA to clipboard                                   |
| ctrl+r | reset cherry-picked (copied) commits selection                 |
| b      | view bisect options                                            |
| s      | squash down                                                    |
| f      | fixup commit                                                   |
| r      | reword commit                                                  |
| R      | reword commit with editor                                      |
| d      | delete commit                                                  |
| e      | edit commit                                                    |
| p      | pick commit (when mid-rebase)                                  |
| F      | create fixup commit for this commit                            |
| S      | squash all 'fixup!' commits above selected commit (autosquash) |
| ctrl+j | move commit down one                                           |
| ctrl+k | move commit up one                                             |
| v      | paste commits (cherry-pick)                                    |
| A      | amend commit with staged changes                               |
| a      | reset commit author                                            |
| t      | revert commit                                                  |
| T      | tag commit                                                     |
| ctrl+l | open log menu                                                  |
| space  | checkout commit                                                |
| y      | copy commit attribute                                          |
| o      | open commit in browser                                         |
| n      | create new branch off of commit                                |
| g      | view reset options                                             |
| c      | copy commit (cherry-pick)                                      |
| C      | copy commit range (cherry-pick)                                |
| enter  | view selected item's files                                     |

## Confirmation Panel

| Key   | Description  |
| ----- | ------------ |
| enter | confirm      |
| esc   | close/cancel |

## Files

| Key    | Description                                                             |
| ------ | ----------------------------------------------------------------------- |
| ctrl+o | copy the file name to the clipboard                                     |
| d      | view 'discard changes' options                                          |
| space  | toggle staged                                                           |
| ctrl+b | Filter files (staged/unstaged)                                          |
| c      | commit changes                                                          |
| w      | commit changes without pre-commit hook                                  |
| A      | amend last commit                                                       |
| C      | commit changes using git editor                                         |
| e      | edit file                                                               |
| o      | open file                                                               |
| i      | ignore or exclude file                                                  |
| r      | refresh files                                                           |
| s      | stash all changes                                                       |
| S      | view stash options                                                      |
| a      | stage/unstage all                                                       |
| enter  | stage individual hunks/lines for file, or collapse/expand for directory |
| g      | view upstream reset options                                             |
| D      | view reset options                                                      |
| `      | toggle file tree view                                                   |
| M      | open external merge tool (git mergetool)                                |
| f      | fetch                                                                   |

## Local Branches

| Key    | Description                                |
| ------ | ------------------------------------------ |
| ctrl+o | copy branch name to clipboard              |
| i      | show git-flow options                      |
| space  | checkout                                   |
| n      | new branch                                 |
| o      | create pull request                        |
| O      | create pull request options                |
| ctrl+y | copy pull request URL to clipboard         |
| c      | checkout by name                           |
| F      | force checkout                             |
| d      | delete branch                              |
| r      | rebase checked-out branch onto this branch |
| M      | merge into currently checked out branch    |
| f      | fast-forward this branch from its upstream |
| T      | create tag                                 |
| g      | view reset options                         |
| R      | rename branch                              |
| u      | set/unset upstream                         |
| enter  | view commits                               |

## Main Panel (Merging)

| Key   | Description                              |
| ----- | ---------------------------------------- |
| e     | edit file                                |
| o     | open file                                |
| ◀     | select previous conflict                 |
| ▶     | select next conflict                     |
| ▲     | select previous hunk                     |
| ▼     | select next hunk                         |
| z     | undo                                     |
| M     | open external merge tool (git mergetool) |
| space | pick hunk                                |
| b     | pick all hunks                           |
| esc   | return to files panel                    |

## Main Panel (Normal)

| Key           | Description         |
| ------------- | ------------------- |
| mouse wheel ▼ | scroll down (fn+up) |
| mouse wheel ▲ | scroll up (fn+down) |

## Main Panel (Patch Building)

| Key    | Description                             |
| ------ | --------------------------------------- |
| ◀      | select previous hunk                    |
| ▶      | select next hunk                        |
| v      | toggle drag select                      |
| V      | toggle drag select                      |
| a      | toggle select hunk                      |
| ctrl+o | copy the selected text to the clipboard |
| o      | open file                               |
| e      | edit file                               |
| space  | add/remove line(s) to patch             |
| esc    | exit custom patch builder               |

## Main Panel (Staging)

| Key    | Description                                     |
| ------ | ----------------------------------------------- |
| ◀      | select previous hunk                            |
| ▶      | select next hunk                                |
| v      | toggle drag select                              |
| V      | toggle drag select                              |
| a      | toggle select hunk                              |
| ctrl+o | copy the selected text to the clipboard         |
| o      | open file                                       |
| e      | edit file                                       |
| esc    | return to files panel                           |
| tab    | switch to other panel (staged/unstaged changes) |
| space  | toggle line staged / unstaged                   |
| d      | delete change (git reset)                       |
| E      | edit hunk                                       |
| c      | commit changes                                  |
| w      | commit changes without pre-commit hook          |
| C      | commit changes using git editor                 |

## Menu

| Key   | Description |
| ----- | ----------- |
| enter | execute     |
| esc   | close       |

## Reflog

| Key    | Description                                    |
| ------ | ---------------------------------------------- |
| ctrl+o | copy commit SHA to clipboard                   |
| space  | checkout commit                                |
| y      | copy commit attribute                          |
| o      | open commit in browser                         |
| n      | create new branch off of commit                |
| g      | view reset options                             |
| c      | copy commit (cherry-pick)                      |
| C      | copy commit range (cherry-pick)                |
| ctrl+r | reset cherry-picked (copied) commits selection |
| enter  | view commits                                   |

## Remote Branches

| Key    | Description                                |
| ------ | ------------------------------------------ |
| ctrl+o | copy branch name to clipboard              |
| space  | checkout                                   |
| n      | new branch                                 |
| M      | merge into currently checked out branch    |
| r      | rebase checked-out branch onto this branch |
| d      | delete branch                              |
| u      | set as upstream of checked-out branch      |
| esc    | Return to remotes list                     |
| g      | view reset options                         |
| enter  | view commits                               |

## Remotes

| Key | Description    |
| --- | -------------- |
| f   | fetch remote   |
| n   | add new remote |
| d   | remove remote  |
| e   | edit remote    |

## Stash

| Key   | Description                |
| ----- | -------------------------- |
| space | apply                      |
| g     | pop                        |
| d     | drop                       |
| n     | new branch                 |
| r     | rename stash               |
| enter | view selected item's files |

## Status

| Key   | Description             |
| ----- | ----------------------- |
| o     | open config file        |
| e     | edit config file        |
| u     | check for update        |
| enter | switch to a recent repo |
| a     | show all branch logs    |

## Sub-commits

| Key    | Description                                    |
| ------ | ---------------------------------------------- |
| ctrl+o | copy commit SHA to clipboard                   |
| space  | checkout commit                                |
| y      | copy commit attribute                          |
| o      | open commit in browser                         |
| n      | create new branch off of commit                |
| g      | view reset options                             |
| c      | copy commit (cherry-pick)                      |
| C      | copy commit range (cherry-pick)                |
| ctrl+r | reset cherry-picked (copied) commits selection |
| enter  | view selected item's files                     |

## Submodules

| Key    | Description                      |
| ------ | -------------------------------- |
| ctrl+o | copy submodule name to clipboard |
| enter  | enter submodule                  |
| d      | remove submodule                 |
| u      | update submodule                 |
| n      | add new submodule                |
| e      | update submodule URL             |
| i      | initialize submodule             |
| b      | view bulk submodule options      |

## Tags

| Key   | Description        |
| ----- | ------------------ |
| space | checkout           |
| d     | delete tag         |
| P     | push tag           |
| n     | create tag         |
| g     | view reset options |
| enter | view commits       |

