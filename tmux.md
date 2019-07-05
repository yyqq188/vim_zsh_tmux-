#### tmux的安装
`sudo apt-get install tmux`
```
要保证tmux是1.9以上的版本
否者安装不了下面的两个插件，这两个插件是为了tmux持久化而用的
```
```
mkdir ~/.tmux
cd ~/.tmux
 git clone https://github.com/tmux-plugins/tmux-resurrect.git

cd ~/.tmux
git clone https://github.com/tmux-plugins/tmux-continuum.git

接着 ， 将以下内容添加到 ~/.tmux.conf：
run-shell ~/.tmux/tmux-resurrect/resurrect.tmux
run-shell ~/.tmux/tmux-continuum/continuum.tmux
```

### .tmux.conf配置文件
```
# 添加的主题配置
set -g default-termina "screen-256color"


#设置session的持久保存和自动保存
run-shell ~/.tmux/tmux-resurrect/resurrect.tmux
run-shell ~/.tmux/tmux-continuum/continuum.tmux
set -g @continuum-save-interval '60'


# 设置成vim模式
setw -g mode-keys vi

# 将面板切换设置成hjkl
bind-key k select-pane -U # up
bind-key j select-pane -D # down
bind-key h select-pane -L # left
bind-key l select-pane -R # right


# 将触发键改成C-a
#set -g prefix C-a
#unbind C-b

# 将复制模式设置成vim的复制模式
bind-key -t vi-copy v begin-selection
bind-key -t vi-copy y copy-pipe "reattach-to-user-namespace pbcopy"

#对于tmux v2.1(2015.10.28)之前的版本，需加入如下配置：
# 
#setw -g mode-mouse on # 支持鼠标选取文本等
#setw -g mouse-resize-pane on # 支持鼠标拖动调整面板的大小(通过拖动面板间的分割线)
#setw -g mouse-select-pane on # 支持鼠标选中并切换面板 
#setw -g mouse-select-window on # 支持鼠标选中并切换窗口(通过点击状态栏窗口名称)

#对于tmux v2.1及以上的版本，仅需加入如下配置：

set-option -g mouse on # 等同于以上4个指令的效果

#默认是zsh
set-option -g default-shell /bin/zsh
#保存文档的行数
set-option -g history-limit 4096

```