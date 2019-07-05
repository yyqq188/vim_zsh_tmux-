#### 1 升级vim7.4到vim8+
`sudo add-apt-repository ppa:jonathonf/vim`
`sudo apt-get update`
`sudo apt-get install vim`
```执行vim --version | grep python  (有python3+ 就说明成功了)```

#### 2 安装 vim-plug
```curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim```

#### 3 安装一些插件的前期安装的程序
##### tagbar 
`sudo apt install ctags`

##### neoformat
`pip install autopep8`

##### ale
`pip install pylint`


#### 4  先执行下面的.vimrc配置中插件的安装
`:source ~/.vimrc`
`:PlugInstall`

#### 5 其中的ycm要在执行插件安装命令后才能编译安装
`cd ~/.vim/plugged/YouCompleteMe`
`./install.py`



### .vimrc配置
```
set hlsearch
set incsearch
set history=1000
set showcmd
set number
set autoindent
set smartindent
let mapleader=','
let &t_Co=256
call plug#begin('~/.vim/plugged')
Plug 'mhinz/vim-startify'
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
Plug 'yggdroot/indentline'
Plug 'morhetz/gruvbox'
Plug 'scrooloose/nerdtree'
Plug 'ctrlpvim/ctrlp.vim'
Plug 'easymotion/vim-easymotion'
Plug 'tpope/vim-surround'
Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }
Plug 'junegunn/fzf.vim'
Plug 'brooth/far.vim'
Plug 'python-mode/python-mode', { 'for': 'python', 'branch': 'develop' }
Plug 'majutsushi/tagbar'
Plug 'lfv89/vim-interestingwords'
Plug 'sbdchd/neoformat'
Plug 'w0rp/ale'
Plug 'tpope/vim-commentary'
Plug 'Valloric/YouCompleteMe'
call plug#end()

" indentline的配置
let g:indentLine_bgcolor_gui = '#FF5F00'
let g:indentLine_concealcursor = 'inc'
let g:indentLine_conceallevel = 2

" 配置gruvbox
colorscheme gruvbox
set background=dark

" 配置nerdtree
nnoremap <leader>v :NERDTreeFind<cr>
nnoremap <leader>g :NERDTreeToggle<cr>
let NERDTreeIgnore = [
    \'\.git$','\.hg$','\.svn$','\.stversions$','\.pyc$','\.pyo$','\.svn$','\.swp$',
    \'\.DS_Store$','\.sass_cache$','__pycache__$','\.egg_info$','\.ropeproject$',
    \]
" 配置ctrlp
let g:ctrlp_map = '<c-p>'
" 配置easymotion
map ss <Plug>(easymotion-s2)

" 配置python-mode
let g:pymode_python = 'python3'
let g:pymode_trim_whitespaces = 1
let g:pymode_doc=1
let g:pymode_doc_bind = 'K'
let g:pymode_rope_goto_definition_bind = "<C-]>"
let g:pymode_lint = 1
let g:pymode_lint_checkers = ['pyflakes','pep8','mccabe','pylint']
let g:pymode_options_max_line_length = 120

" 配置tagbarToggle
map<F3> :TagbarToggle<CR>

" 配置格式静态检查
map<F9> :Neoformat<CR>

" 配置高亮关键词
let g:interestingWordsGUIColors = ['#8CCBEA', '#A4E57E', '#FFDB72', '#FF7272', '#FFB3FF', '#9999FF']
let g:interestingWordsTermColors = ['154', '121', '211', '137', '214', '222']
let g:interestingWordsRandomiseColors = 1

" 配置ycm
"默认配置文件路径"
let g:ycm_global_ycm_extra_conf = '.vim/plugged/YouCompleteMe/third_party/ycmd/.ycm_extra_conf.py'
" 设置在下面几种格式的文件上屏蔽ycm
let g:ycm_filetype_blacklist = {
        \ 'tagbar' : 1,
        \ 'nerdtree' : 1,
	\}


" 一键运行python 按F5
map <F5> :call CompileRunGcc()<CR>
    func! CompileRunGcc()
        exec "w"
if &filetype == 'c'
            exec "!g++ % -o %<"
            exec "!time ./%<"
elseif &filetype == 'cpp'
            exec "!g++ % -o %<"
            exec "!time ./%<"
elseif &filetype == 'java'
            exec "!javac %"
            exec "!time java %<"
elseif &filetype == 'sh'
            :!time bash %
elseif &filetype == 'python'
            exec "!time python %"
elseif &filetype == 'html'
            exec "!firefox % &"
elseif &filetype == 'go'
    "        exec "!go build %<"
            exec "!time go run %"
elseif &filetype == 'mkd'
            exec "!~/.vim/markdown.pl % > %.html &"
            exec "!firefox %.html &"
endif
    endfunc
```

