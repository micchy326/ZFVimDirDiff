# ZFVimDirDiff

vim script to diff two directories like BeyondCompare by using `diff`

inspired from [will133/vim-dirdiff](https://github.com/will133/vim-dirdiff)

* why another reproduce?

    * format the `diff` result and output as vertical split file tree view,
        which should be more human-readable
    * more friendly file sync operation, keep same habit with vim's builtin `diff`

![](https://raw.githubusercontent.com/ZSaberLv0/ZFVimDirDiff/master/preview.png)

if you like my work, [check here](https://github.com/ZSaberLv0?utf8=%E2%9C%93&tab=repositories&q=ZFVim) for a list of my vim plugins


# how to use

1. install by [vim-plug](https://github.com/junegunn/vim-plug) or any other plugin manager:

    ```
    Plug 'ZSaberLv0/ZFVimDirDiff'
    ```

1. use `:ZFDirDiff` command to start diff

    ```
    :ZFDirDiff pathA pathB
    ```

1. within the diff window:

    * use `DD` to update the diff result
    * use `o` or `<cr>` to open file diff
    * use `do` or `DH` to sync from another side to current side
    * use `dp` or `DL` to sync from current side to another side
    * use `dd` to delete node under cursor
    * use `p` to copy the node's path, and `P` for the node's full path
    * use `q` to exit diff
    * recommend to use [ZSaberLv0/ZFVimIndentMove](https://github.com/ZSaberLv0/ZFVimIndentMove)
        or [easymotion/vim-easymotion](https://github.com/easymotion/vim-easymotion)
        to quickly move between file tree node


# configs

* for core logic:
    * `let g:ZFDirDiffShowSameFile = 1` : whether to show files that are same
    * `let g:ZFDirDiffFileExclude = ''` : file name exclude pattern, e.g. `*.class,*.o`

        typical setting:

        ```
        let g:ZFDirDiffFileExclude = 'tags'
        let g:ZFDirDiffFileExclude .= ',*.swp'
        let g:ZFDirDiffFileExclude .= ',.DS_Store'
        let g:ZFDirDiffFileExclude .= ',*.d'
        let g:ZFDirDiffFileExclude .= ',*.depend*'
        let g:ZFDirDiffFileExclude .= ',*.a'
        let g:ZFDirDiffFileExclude .= ',*.o'
        let g:ZFDirDiffFileExclude .= ',*.so'
        let g:ZFDirDiffFileExclude .= ',*.dylib'
        let g:ZFDirDiffFileExclude .= ',*.jar'
        let g:ZFDirDiffFileExclude .= ',*.class'
        let g:ZFDirDiffFileExclude .= ',*.exe'
        let g:ZFDirDiffFileExclude .= ',*.dll'
        let g:ZFDirDiffFileExclude .= ',*.iml'
        let g:ZFDirDiffFileExclude .= ',local.properties'
        let g:ZFDirDiffFileExclude .= ',*.user'

        let g:ZFDirDiffFileExclude .= ',*/.svn/*'
        let g:ZFDirDiffFileExclude .= ',*/.git/*'
        let g:ZFDirDiffFileExclude .= ',*/.hg/*'
        let g:ZFDirDiffFileExclude .= ',*/.cache/*'
        let g:ZFDirDiffFileExclude .= ',*/_cache/*'
        let g:ZFDirDiffFileExclude .= ',*/.tmp/*'
        let g:ZFDirDiffFileExclude .= ',*/_tmp/*'
        let g:ZFDirDiffFileExclude .= ',*/.release/*'
        let g:ZFDirDiffFileExclude .= ',*/_release/*'
        let g:ZFDirDiffFileExclude .= ',*/.build/*'
        let g:ZFDirDiffFileExclude .= ',*/_build/*'
        let g:ZFDirDiffFileExclude .= ',*/build-*/*'
        let g:ZFDirDiffFileExclude .= ',*/bin-*/*'
        let g:ZFDirDiffFileExclude .= ',*/_repo/*'
        let g:ZFDirDiffFileExclude .= ',*/.wing/*'
        let g:ZFDirDiffFileExclude .= ',*/.idea/*'
        let g:ZFDirDiffFileExclude .= ',*/.gradle/*'
        let g:ZFDirDiffFileExclude .= ',*/build/*'
        let g:ZFDirDiffFileExclude .= ',*/.externalNativeBuild/*'
        let g:ZFDirDiffFileExclude .= ',*/Pods/*'
        let g:ZFDirDiffFileExclude .= ',*/vendor/*'
        ```

    * `let g:ZFDirDiffContentExclude = ''` : file content exclude pattern, e.g. `log:,id:`
    * `let g:ZFDirDiffFileIgnoreCase = 0` : whether ignore file name case
    * `let g:ZFDirDiffCustomDiffArg = ''` : additional diff args passed to `diff`
    * `let g:ZFDirDiffSortFunc = 'ZF_DirDiffSortFunc'` : sort function
* for builtin UI impl:
    * `let g:ZFDirDiffUI_filetypeLeft = 'ZFDirDiffLeft'` : `filetype` for left diff buffer
    * `let g:ZFDirDiffUI_filetypeRight = 'ZFDirDiffRight'` : `filetype` for right diff buffer
    * `let g:ZFDirDiffUI_tabstop = 2` : `tabstop` for diff buffer
    * `let g:ZFDirDiffUI_headerTextFunc = 's:headerText'` : function name to get the header text

        ```
        " return a list of strings
        function! YourFunc(isLeft, fileLeft, fileRight)
            return []
        endfunction
        ```

    * `let g:ZFDirDiffUI_syncSameFile = 0` : whether need to sync same file
    * whether confirm before sync
        * `let g:ZFDirDiffConfirmSyncDir = 1`
        * `let g:ZFDirDiffConfirmSyncFile = 1`
        * `let g:ZFDirDiffConfirmSyncConflict = 1`
        * `let g:ZFDirDiffConfirmCopyDir = 1`
        * `let g:ZFDirDiffConfirmCopyFile = 0`
        * `let g:ZFDirDiffConfirmRemoveDir = 1`
        * `let g:ZFDirDiffConfirmRemoveFile = 1`
    * keymaps
        * `let g:ZFDirDiffKeymap_update = ['DD']`
        * `let g:ZFDirDiffKeymap_open = ['<cr>', 'o']`
        * `let g:ZFDirDiffKeymap_goParent = ['u']`
        * `let g:ZFDirDiffKeymap_quit = ['q']`
        * `let g:ZFDirDiffKeymap_quitDiff = ['q']`
        * `let g:ZFDirDiffKeymap_nextDiff = [']c', 'DJ']`
        * `let g:ZFDirDiffKeymap_prevDiff = ['[c', 'DK']`
        * `let g:ZFDirDiffKeymap_syncToHere = ['do', 'DH']`
        * `let g:ZFDirDiffKeymap_syncToThere = ['dp', 'DL']`
        * `let g:ZFDirDiffKeymap_deleteFile = ['dd']`
        * `let g:ZFDirDiffKeymap_getPath = ['p']`
        * `let g:ZFDirDiffKeymap_getFullPath = ['P']`
    * highlight

        ```
        highlight! link ZFDirDiffHL_Title Title
        highlight! link ZFDirDiffHL_Dir Directory
        highlight! link ZFDirDiffHL_Diff DiffText
        highlight! link ZFDirDiffHL_DirOnlyHere DiffAdd
        highlight! link ZFDirDiffHL_DirOnlyThere Normal
        highlight! link ZFDirDiffHL_FileOnlyHere DiffAdd
        highlight! link ZFDirDiffHL_FileOnlyThere Normal
        highlight! link ZFDirDiffHL_ConflictDir ErrorMsg
        highlight! link ZFDirDiffHL_ConflictFile WarningMsg
        ```

