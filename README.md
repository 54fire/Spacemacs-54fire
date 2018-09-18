<h1 align="center"> 54fire‘s Spacemacs config </h1>

I love Spacemacs,it very nice!

## w3m emms
1. w3m 用于在emacs中浏览网页。
    - 在mac中先安装w3m
        ```
        brew install w3m
        ```
    - 在emacs中安装w3m的package。
2. emms 用于在emacs中播放音乐或者视频
    - 在mac中先安装mplayer
      ```
      brew install mplayer
      ```
    - 在emacs中安装emms的package.

## PDF
1. 使用插件pdf-tools
    - 安装插件后再配置文件中键入`(pdf-tools-install)`
2. 其中要关闭global-linum-mode,否则可能导致emacs崩溃。
3. 使用Spacemacs可以将配置修改为：
  ```lisp
  dotspacemacs-line-numbers '(:disabled-for-modes dired-mode
                                                  doc-view-mode
                                                  markdown-mode
                                                  org-mode
                                                  pdf-view-mode
                             )
  ```
4. 命令行:  
    - `M-x pdf-tools-help RET` 打开pdf-tools的帮助页面
    - `M-x pdf-tools-customize RET` 打开自定义页面
    
## recentf
1. 使用`SPC f r`进入recentf mode
    - `C-n` 向下移动
    - `C-p` 向上移动 

## Neotree
1. 打开与关闭操作：
    - `SPC f t` 打开和关闭
2. 使用帮助
    - `?` 打开Neotree的帮助页面
3. 基础操作
    - `h` 合并目录
    - `j` 向下移动
    - `k` 向上移动
    - `l` 展开目录，如果是文档将打开

## Windows
1. 分屏操作：
    - `SPC w s` or `SPC w /` 竖直分屏
    - `SPC w v` or `SPC w -` 水平分屏
    
2. 光标在window中的切换
    - `SPC w h` 光标切换到左窗口
    - `SPC w j` 光标切换到下窗口
    - `SPC w k` 光标切换到上窗口
    - `SPC w l` 光标切换到右窗口
3. 删除当前光标所在窗口
    - `SPC w d` 删除当前光标所在窗口

## Dired-mode
1. Dired Mode 是一个强大的模式它能让我们完成和文件管理相关的所有操作。

2. 使用`C-x d` or `SPC j d`就可以进入Dired Mode，其常用操作如下：
  - `+` 创建目录
  - `g` 刷新目录
  - `C` 拷贝
  - `D` 删除
  - `R` 重命名
  - `d` 标记删除
  - `u` 取消标记
  - `x` 执行所以标记

3. 这里有几点可以优化的地方。
    1. 第一是删除目录的时候 Emacs 会询问是否递归删除或拷贝， 这也有些麻烦我们可以用下面的配置将其设定为默认递归删除目录（出于安全原因的考虑， 也许你需要保持此行为。所有文中的配置请务必按需配置）。
      ```lisp
      (setq dired-recursive-deletes 'always)
      (setq dired-recursive-copies 'always)
      ```

    2. 第二是每一次你进入一个回车进入一个新的目录中，一个新的缓冲区就会被建立。这使得我们的缓冲区列表中充满了大量没有实际意义的记录。我们可以使用下面的代码，让 Emacs 重用唯一的一个缓冲区作为Dired Mode显示专用缓冲区。
      ```lisp
      (put 'dired-find-alternate-file 'disabled nil)
      ;; 主动加载 Dired Mode
      ;; (require 'dired)
      ;; (defined-key dired-mode-map (kbd "o") 'dired-find-alternate-file)

      ;; 延迟加载.点击o键就可以打开目录。。(根据个人习惯设置)
      (with-eval-after-load 'dired
          (define-key dired-mode-map (kbd "o") 'dired-find-alternate-file))
      ```
      使用延迟加载可以使编辑器加载速度有所提升。

    3. 启用 dired-x 可以让每一次进入 Dired 模式时，使用新的快捷键 `C-x C-j` 就可以进 入当前文件夹的所在的路径。
      ```lisp
      (require 'dired-x)
      ```
    4. 使用 `(setq dired-dwin-target 1)` 则可以使当一个窗口（frame）中存在两个分屏 （window）时，将另一个分屏自动设置成拷贝地址的目标。
