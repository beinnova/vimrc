set encoding=utf-8                      " The encoding displayed.
set fileencoding=utf-8                  " The encoding written to file.
"set tabstop=4 shiftwidth=4 expandtab    " Insert spaces whne tab is pressed
cd /home/josh/workspace/xara/ " default workdir
set nocompatible                        " be iMproved, required
filetype off                            " required
syntax on                               " Enable config
set number                              " Set line numbers
set cursorline                          " Set corson as line
highlight LineNr guifg=#050505          

"set tags=./tags;,tags;
:let g:easytags_file = './tags'

" ======= Vuble =========
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" let Vundle manage Vundle, required
Plugin 'majutsushi/tagbar'
Plugin 'vim-syntastic/syntastic'
Plugin 'vim-airline/vim-airline'
Plugin 'vim-airline/vim-airline-themes'
Plugin 'scrooloose/nerdtree'
Plugin 'tpope/vim-fugitive'
Plugin 'VundleVim/Vundle.vim'
Plugin 'Valloric/YouCompleteMe'
Plugin 'jelera/vim-javascript-syntax'
Plugin 'pangloss/vim-javascript'
Plugin 'jdkanani/vim-material-theme'
Plugin 'tobyS/vmustache'
Plugin 'tobyS/pdv'
Plugin 'maksimr/vim-jsbeautify'
Plugin 'xolox/vim-misc'
Plugin 'kien/ctrlp.vim'
Plugin 'djjcast/mirodark'
Plugin 'ekalinin/Dockerfile.vim'
Plugin 'arcticicestudio/nord-vim'
Plugin 'edkolev/tmuxline.vim'    "tmuxline

call vundle#end()            " required
" ===== Vundle =====

" Set editor configuration
filetype plugin indent on    " required
set background=dark

"colorscheme material-theme 
if has('gui_running')
    colorscheme nord
    set lines=999 columns=999
else
    colorscheme nord
endif

"Opne NERDTree only if no file is in edit
"autocmd StdinReadPre * let s:std_in=1
"autocmd VimEnter * if argc() == 0 && !exists("s:std_in") | NERDTree | endif

" ***Map keyword***
" Move across the tabs
nnoremap <silent> <A-Up> :wincmd k<CR>
nnoremap <silent> <A-Down> :wincmd j<CR>
nnoremap <silent> <A-Left> :wincmd h<CR>:
nnoremap <silent> <A-Right> :wincmd l<CR>
map <leader>r :NERDTreeFind<CR>

autocmd FileType javascript noremap <buffer>  <c-f> :call JsBeautify()<cr>
autocmd FileType json noremap <buffer> <c-f> :call JsonBeautify()<cr>
autocmd FileType jsx noremap <buffer> <c-f> :call JsxBeautify()<cr>
autocmd FileType html noremap <buffer> <c-f> :call HtmlBeautify()<cr>
autocmd FileType css noremap <buffer> <c-f> :call CSSBeautify()<cr>

"Open project property 
nmap <F8> :TagbarToggle<CR>
"Open NERDTree
nmap <F3> :NERDTree<CR>

" ***End Map****
" ***GOLANG Tag***
"let g:tagbar_type_go = {
"    \ 'ctagstype': 'go',
"    \ 'kinds' : [
"        \'p:package',
"        \'f:function',
"        \'v:variables',
"        \'t:type',
"        \'c:const'
"    \]
"  \}
"
"
" Vim Airline Config
let g:airline#extensions#tabline#enabled = 1
let g:airline_powerline_fonts = 1
let g:airline_theme='molokai'

"Set header on files
"JS headers
autocmd bufnewfile *.js so $HOME/.vim/templates/js/header
"autocmd bufnewfile *.js exe "1," . 9 . "g/File Name :.*/s//File Name : " .expand('%:t')
"autocmd bufnewfile *.js exe "1," . 9 . "g/On :.*/s//On : " .strftime("%d-%m-%Y")
"autocmd bufnewfile *.js exe "1," . 9 . "g/At :.*/s//At : " .strftime("%H:%M")
autocmd bufwritepost,filewritepost *.js execute "normal ma"
"Gitignore
autocmd bufnewfile .gitignore so $HOME/.vim/templates/common/gitignore
autocmd bufwritepost,filewritepost .gitignore execute "normal ma"


let g:ctrlp_working_path_mode = 'ra'
let g:ctrlp_custom_ignore = {
  \ 'dir':  '\v[\/](.git|node_modules|bower_componets|vendor)$'
  \ }
let g:php_syntax_extensions_enabled = 1
let b:php_syntax_extensions_enabled = 1
let g:pdv_template_dir = $HOME."/.vim/bundle/pdv/templates/"
nnoremap <buffer> <Leader>p :call pdv#DocumentCurrentLine()<CR>
" folding
set foldmethod=syntax
set foldlevelstart=1

let javaScript_fold=1	      "JavaScript
let sh_fold_enabled=1         " sh
"
"Show status bar always
set laststatus=2 
"set statusline+=%F
:nnoremap <Tab> :bnext<CR>
:nnoremap <S-Tab> :bprevious<CR>
set statusline+=%#warningmsg#
set statusline+=%{SyntasticStatuslineFlag()}
set statusline+=%*

let g:syntastic_always_populate_loc_list = 1
let g:syntastic_auto_loc_list = 1
let g:syntastic_check_on_open = 1
let g:syntastic_check_on_wq = 0
"let g:syntastic_javascript_checkers = ['eslint']
let g:syntastic_javascript_checkers = []
autocmd FileType javascript let b:syntastic_checkers = findfile('.eslintrc', '.;') !=# '' ? ['eslint'] : []
"let g:syntastic_debug = 3
set foldmethod
