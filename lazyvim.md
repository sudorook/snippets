# LazyVim Keymap

**LazyVim** uses [which-key.nvim](https://github.com/folke/which-key.nvim) to
help you remember your keymaps. Just press any key like `<space>` and you'll see
a popup with all possible keymaps starting with `<space>`.

## General

| Key                | Description                           | Mode       |
| ------------------ | ------------------------------------- | ---------- |
| <C-h>              | Go to left window                     | n          |
| <C-j>              | Go to lower window                    | n          |
| <C-k>              | Go to upper window                    | n          |
| <C-l>              | Go to right window                    | n          |
| <C-Up>             | Increase window height                | n          |
| <C-Down>           | Decrease window height                | n          |
| <C-Left>           | Decrease window width                 | n          |
| <C-Right>          | Increase window width                 | n          |
| <A-j>              | Move down                             | n, i, v    |
| <A-k>              | Move up                               | n, i, v    |
| <S-h>              | Prev buffer                           | n          |
| <S-l>              | Next buffer                           | n          |
| [b                 | Prev buffer                           | n          |
| ]b                 | Next buffer                           | n          |
| <leader>bb         | Switch to Other Buffer                | n          |
| <leader>`          | Switch to Other Buffer                | n          |
| <esc>              | Escape and clear hlsearch             | i, n       |
| <leader>ur         | Redraw / clear hlsearch / diff update | n          |
| gw                 | Search word under cursor              | n, x       |
| n                  | Next search result                    | n, x, o    |
| N                  | Prev search result                    | n, x, o    |
| <C-s>              | Save file                             | i, v, n, s |
| <leader>l          | Lazy                                  | n          |
| <leader>fn         | New File                              | n          |
| <leader>xl         | Location List                         | n          |
| <leader>xq         | Quickfix List                         | n          |
| <leader>uf         | Toggle format on Save                 | n          |
| <leader>us         | Toggle Spelling                       | n          |
| <leader>uw         | Toggle Word Wrap                      | n          |
| <leader>ul         | Toggle Line Numbers                   | n          |
| <leader>ud         | Toggle Diagnostics                    | n          |
| <leader>uc         | Toggle Conceal                        | n          |
| <leader>gg         | Lazygit (root dir)                    | n          |
| <leader>gG         | Lazygit (cwd)                         | n          |
| <leader>qq         | Quit all                              | n          |
| <leader>ui         | Inspect Pos                           | n          |
| <leader>ft         | Terminal (root dir)                   | n          |
| <leader>fT         | Terminal (cwd)                        | n          |
| <esc><esc>         | Enter Normal Mode                     | t          |
| <leader>ww         | Other window                          | n          |
| <leader>wd         | Delete window                         | n          |
| <leader>w-         | Split window below                    | n          |
| <leader>w\|        | Split window right                    | n          |
| <leader>-          | Split window below                    | n          |
| <leader>\|         | Split window right                    | n          |
| <leader><tab>l     | Last Tab                              | n          |
| <leader><tab>f     | First Tab                             | n          |
| <leader><tab><tab> | New Tab                               | n          |
| <leader><tab>]     | Next Tab                              | n          |
| <leader><tab>d     | Close Tab                             | n          |
| <leader><tab>[     | Previous Tab                          | n          |

## LSP

| Key        | Description            | Mode |
| ---------- | ---------------------- | ---- |
| <leader>cd | Line Diagnostics       | n    |
| <leader>cl | Lsp Info               | n    |
| gd         | Goto Definition        | n    |
| gr         | References             | n    |
| gD         | Goto Declaration       | n    |
| gI         | Goto Implementation    | n    |
| gy         | Goto T[y]pe Definition | n    |
| K          | Hover                  | n    |
| gK         | Signature Help         | n    |
| <c-k>      | Signature Help         | i    |
| ]d         | Next Diagnostic        | n    |
| [d         | Prev Diagnostic        | n    |
| ]e         | Next Error             | n    |
| [e         | Prev Error             | n    |
| ]w         | Next Warning           | n    |
| [w         | Prev Warning           | n    |
| <leader>cf | Format Document        | n    |
| <leader>cf | Format Range           | v    |
| <leader>ca | Code Action            | n, v |
| <leader>cA | Source Action          | n    |
| <leader>cr | Rename                 | n    |

## [bufferline.nvim](https://github.com/akinsho/bufferline.nvim.git)

| Key        | Description               | Mode |
| ---------- | ------------------------- | ---- |
| <leader>bp | Toggle pin                | n    |
| <leader>bP | Delete non-pinned buffers | n    |

## [flit.nvim](https://github.com/ggandor/flit.nvim.git)

| Key | Description | Mode    |
| --- | ----------- | ------- |
| f   | f           | n, x, o |
| F   | F           | n, x, o |
| t   | t           | n, x, o |
| T   | T           | n, x, o |

## [leap.nvim](https://github.com/ggandor/leap.nvim.git)

| Key | Description       | Mode    |
| --- | ----------------- | ------- |
| s   | Leap forward to   | n, x, o |
| S   | Leap backward to  | n, x, o |
| gs  | Leap from windows | n, x, o |

## [mason.nvim](https://github.com/williamboman/mason.nvim.git)

| Key        | Description | Mode |
| ---------- | ----------- | ---- |
| <leader>cm | Mason       | n    |

## [mini.bufremove](https://github.com/echasnovski/mini.bufremove.git)

| Key        | Description           | Mode |
| ---------- | --------------------- | ---- |
| <leader>bd | Delete Buffer         | n    |
| <leader>bD | Delete Buffer (Force) | n    |

## [mini.surround](https://github.com/echasnovski/mini.surround.git)

| Key | Description                          | Mode |
| --- | ------------------------------------ | ---- |
| gza | Add surrounding                      | n, v |
| gzd | Delete surrounding                   | n    |
| gzf | Find right surrounding               | n    |
| gzF | Find left surrounding                | n    |
| gzh | Highlight surrounding                | n    |
| gzr | Replace surrounding                  | n    |
| gzn | Update `MiniSurround.config.n_lines` | n    |

## [neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim.git)

| Key        | Description                 | Mode |
| ---------- | --------------------------- | ---- |
| <leader>fe | Explorer NeoTree (root dir) | n    |
| <leader>fE | Explorer NeoTree (cwd)      | n    |
| <leader>e  | Explorer NeoTree (root dir) | n    |
| <leader>E  | Explorer NeoTree (cwd)      | n    |

## [noice.nvim](https://github.com/folke/noice.nvim.git)

| Key         | Description        | Mode    |
| ----------- | ------------------ | ------- |
| <S-Enter>   | Redirect Cmdline   | c       |
| <leader>snl | Noice Last Message | n       |
| <leader>snh | Noice History      | n       |
| <leader>sna | Noice All          | n       |
| <leader>snd | Dismiss All        | n       |
| <c-f>       | Scroll forward     | i, n, s |
| <c-b>       | Scroll backward    | i, n, s |

## [nvim-notify](https://github.com/rcarriga/nvim-notify.git)

| Key        | Description              | Mode |
| ---------- | ------------------------ | ---- |
| <leader>un | Delete all Notifications | n    |

## [nvim-spectre](https://github.com/nvim-pack/nvim-spectre.git)

| Key        | Description                | Mode |
| ---------- | -------------------------- | ---- |
| <leader>sr | Replace in files (Spectre) | n    |

## [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter.git)

| Key       | Description         | Mode |
| --------- | ------------------- | ---- |
| <c-space> | Increment selection | n    |
| <bs>      | Decrement selection | x    |

## [persistence.nvim](https://github.com/folke/persistence.nvim.git)

| Key        | Description                | Mode |
| ---------- | -------------------------- | ---- |
| <leader>qs | Restore Session            | n    |
| <leader>ql | Restore Last Session       | n    |
| <leader>qd | Don't Save Current Session | n    |

## [telescope.nvim](https://github.com/nvim-telescope/telescope.nvim.git)

| Key             | Description              | Mode |
| --------------- | ------------------------ | ---- |
| <leader>,       | Switch Buffer            | n    |
| <leader>/       | Grep (root dir)          | n    |
| <leader>:       | Command History          | n    |
| <leader><space> | Find Files (root dir)    | n    |
| <leader>fb      | Buffers                  | n    |
| <leader>ff      | Find Files (root dir)    | n    |
| <leader>fF      | Find Files (cwd)         | n    |
| <leader>fr      | Recent                   | n    |
| <leader>fR      | Recent (cwd)             | n    |
| <leader>gc      | commits                  | n    |
| <leader>gs      | status                   | n    |
| <leader>sa      | Auto Commands            | n    |
| <leader>sb      | Buffer                   | n    |
| <leader>sc      | Command History          | n    |
| <leader>sC      | Commands                 | n    |
| <leader>sd      | Document diagnostics     | n    |
| <leader>sD      | Workspace diagnostics    | n    |
| <leader>sg      | Grep (root dir)          | n    |
| <leader>sG      | Grep (cwd)               | n    |
| <leader>sh      | Help Pages               | n    |
| <leader>sH      | Search Highlight Groups  | n    |
| <leader>sk      | Key Maps                 | n    |
| <leader>sM      | Man Pages                | n    |
| <leader>sm      | Jump to Mark             | n    |
| <leader>so      | Options                  | n    |
| <leader>sR      | Resume                   | n    |
| <leader>sw      | Word (root dir)          | n    |
| <leader>sW      | Word (cwd)               | n    |
| <leader>uC      | Colorscheme with preview | n    |
| <leader>ss      | Goto Symbol              | n    |
| <leader>sS      | Goto Symbol (Workspace)  | n    |

### Default Telescope mappings

| Mappings        | Action                                               |
| --------------- | ---------------------------------------------------- |
| <C-n> or <Down> | Next item                                            |
| <C-p> or <Up>   | Previous item                                        |
| j               | Next (in normal mode)                                |
| k               | Previous (in normal mode)                            |
| H               | Select High (in normal mode)                         |
| M               | Select Middle (in normal mode)                       |
| L               | Select Low (in normal mode)                          |
| gg              | Select the first item (in normal mode)               |
| G               | Select the last item (in normal mode)                |
| <CR>            | Confirm selection                                    |
| <C-x>           | Go to file selection as a split                      |
| <C-v>           | Go to file selection as a vsplit                     |
| <C-t>           | Go to a file in a new tab                            |
| <C-u>           | Scroll up in preview window                          |
| <C-d>           | Scroll down in preview window                        |
| <C-/>           | Show mappings for picker actions (insert mode)       |
| ?               | Show mappings for picker actions (normal mode)       |
| <C-c>           | Close telescope                                      |
| <Esc>           | Close telescope (in normal mode)                     |
| <Tab>           | Toggle selection and move to next selection          |
| <S-Tab>         | Toggle selection and move to prev selection          |
| <C-q>           | Send all items not filtered to quickfixlist (qflist) |
| <M-q>           | Send all selected items to qflist                    |

## [todo-comments.nvim](https://github.com/folke/todo-comments.nvim.git)

| Key        | Description              | Mode |
| ---------- | ------------------------ | ---- |
| ]t         | Next todo comment        | n    |
| [t         | Previous todo comment    | n    |
| <leader>xt | Todo (Trouble)           | n    |
| <leader>xT | Todo/Fix/Fixme (Trouble) | n    |
| <leader>st | Todo                     | n    |
| <leader>sT | Todo/Fix/Fixme           | n    |

## [trouble.nvim](https://github.com/folke/trouble.nvim.git)

| Key        | Description                     | Mode |
| ---------- | ------------------------------- | ---- |
| <leader>xx | Document Diagnostics (Trouble)  | n    |
| <leader>xX | Workspace Diagnostics (Trouble) | n    |
| <leader>xL | Location List (Trouble)         | n    |
| <leader>xQ | Quickfix List (Trouble)         | n    |
| [q         | Previous trouble/quickfix item  | n    |
| ]q         | Next trouble/quickfix item      | n    |

## [vim-illuminate](https://github.com/RRethy/vim-illuminate.git)

| Key | Description    | Mode |
| --- | -------------- | ---- |
| ]]  | Next Reference | n    |
| [[  | Prev Reference | n    |

## [nvim-dap](https://github.com/mfussenegger/nvim-dap.git)

Part of [lazyvim.plugins.extras.dap.core](/plugins/extras/dap.core)

| Key        | Description             | Mode |
| ---------- | ----------------------- | ---- |
| <leader>dB | Breakpoint Condition    | n    |
| <leader>db | Toggle Breakpoint       | n    |
| <leader>dc | Continue                | n    |
| <leader>dC | Run to Cursor           | n    |
| <leader>dg | Go to line (no execute) | n    |
| <leader>di | Step Into               | n    |
| <leader>dj | Down                    | n    |
| <leader>dk | Up                      | n    |
| <leader>dl | Run Last                | n    |
| <leader>do | Step Out                | n    |
| <leader>dO | Step Over               | n    |
| <leader>dp | Pause                   | n    |
| <leader>dr | Toggle REPL             | n    |
| <leader>ds | Session                 | n    |
| <leader>dt | Terminate               | n    |
| <leader>dw | Widgets                 | n    |

## [nvim-dap-ui](https://github.com/rcarriga/nvim-dap-ui.git)

Part of [lazyvim.plugins.extras.dap.core](/plugins/extras/dap.core)

| Key        | Description | Mode |
| ---------- | ----------- | ---- |
| <leader>du | Dap UI      | n    |
| <leader>de | Eval        | n, v |

## [one-small-step-for-vimkind](https://github.com/jbyuki/one-small-step-for-vimkind.git)

Part of [lazyvim.plugins.extras.dap.nlua](/plugins/extras/dap.nlua)

| Key         | Description        | Mode |
| ----------- | ------------------ | ---- |
| <leader>daL | Adapter Lua Server | n    |
| <leader>dal | Adapter Lua        | n    |

## [project.nvim](https://github.com/ahmedkhalf/project.nvim.git)

Part of [lazyvim.plugins.extras.util.project](/plugins/extras/util.project)

| Key        | Description | Mode |
| ---------- | ----------- | ---- |
| <leader>fp | Projects    | n    |

## Extra Plugins

### Comment.nvim

Taken from [Comment.nvim](https://github.com/numToStr/Comment.nvim).

#### Basic mappings

These mappings are enabled by default. (config: mappings.basic)

**NORMAL mode**

| Shortcut            | Description                                                        |
| ------------------- | ------------------------------------------------------------------ |
| `gcc`               | Toggles the current line using linewise comment                    |
| `gbc`               | Toggles the current line using blockwise comment                   |
| `[count]gcc`        | Toggles the number of line given as a prefix-count using linewise  |
| `[count]gbc`        | Toggles the number of line given as a prefix-count using blockwise |
| `gc[count]{motion}` | (Op-pending) Toggles the region using linewise comment             |
| `gb[count]{motion}` | (Op-pending) Toggles the region using blockwise comment            |

**VISUAL mode**

| Shortcut | Description                                |
| -------- | ------------------------------------------ |
| `gc`     | Toggles the region using linewise comment  |
| `gb`     | Toggles the region using blockwise comment |

#### Extra mappings

These mappings are enabled by default. (config: mappings.extra)

**NORMAL mode**

| Shortcut | Description                                                      |
| -------- | ---------------------------------------------------------------- |
| `gco`    | Insert comment to the next line and enters INSERT mode           |
| `gcO`    | Insert comment to the previous line and enters INSERT mode       |
| `gcA`    | Insert comment to end of the current line and enters INSERT mode |

Examples

# Linewise

| Shortcut | Description                                                |
| -------- | ---------------------------------------------------------- |
| `gcw`    | Toggle from the current cursor position to the next word   |
| `gc$`    | Toggle from the current cursor position to the end of line |
| `gc}`    | Toggle until the next blank line                           |
| `gc5j`   | Toggle 5 lines after the current cursor position           |
| `gc8k`   | Toggle 8 lines before the current cursor position          |
| `gcip`   | Toggle inside of paragraph                                 |
| `gca}`   | Toggle around curly brackets                               |

# Blockwise

| Shortcut | Description                                                  |
| -------- | ------------------------------------------------------------ |
| `gb2}`   | Toggle until the 2 next blank line                           |
| `gbaf`   | Toggle comment around a function (w/ LSP/treesitter support) |
