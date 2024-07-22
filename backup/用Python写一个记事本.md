> [!WARNING]
> 这个记事本无法选择保存格式，不过玩一玩也是可以的

> [!WARNING]
> 用Python的IDLE新建项目写！用Python的IDLE新建项目写！用Python的IDLE新建项目写！

> [!TIP]
>结尾有一个精简版，可以看一看

代码如下：
```python
import tkinter as tk
from tkinter import filedialog, messagebox, simpledialog, colorchooser
class Notepad:
    def __init__(self, root):
        self.root = root
        self.root.title("记事本")
        
        self.text = tk.Text(self.root, undo=True)
        self.text.pack(expand=True, fill='both')
        
        menu = tk.Menu(self.root)
        
        file_menu = tk.Menu(menu, tearoff=0)
        file_menu.add_command(label="新建", command=self.new_file)
        file_menu.add_command(label="打开", command=self.open_file)
        file_menu.add_command(label="保存", command=self.save_file)
        file_menu.add_command(label="另存", command=self.save_as_file)
        file_menu.add_command(label="退出", command=self.exit)
        menu.add_cascade(label="文件", menu=file_menu)
        
        edit_menu = tk.Menu(menu, tearoff=0)
        edit_menu.add_command(label="复制", command=self.copy)
        edit_menu.add_command(label="粘贴", command=self.paste)
        edit_menu.add_command(label="剪切", command=self.cut)
        edit_menu.add_command(label="替换", command=self.replace)
        menu.add_cascade(label="编辑", menu=edit_menu)
        
        format_menu = tk.Menu(menu, tearoff=0)
        format_menu.add_command(label="设置字号", command=self.set_font_size)
        format_menu.add_command(label="设置背景", command=self.set_bg_color)
        format_menu.add_command(label="设置字色", command=self.set_fg_color)
        menu.add_cascade(label="格式", menu=format_menu)
        
        self.root.config(menu=menu)
        
    def new_file(self):
        self.text.delete('1.0', tk.END)
        
    def open_file(self):
        file = filedialog.askopenfile(mode='r')
        if file is not None:
            self.text.delete('1.0', tk.END)
            self.text.insert(tk.INSERT, file.read())
            file.close()
            
    def save_file(self):
        file = filedialog.asksaveasfile(mode='w')
        if file is not None:
            file.write(self.text.get('1.0', tk.END))
            file.close()
            
    def save_as_file(self):
        file = filedialog.asksaveasfile(mode='w')
        if file is not None:
            file.write(self.text.get('1.0', tk.END))
            file.close()
            
    def exit(self):
        self.root.destroy()
        
    def copy(self):
        self.text.clipboard_clear()
        self.text.clipboard_append(self.text.selection_get())
        
    def paste(self):
        self.text.insert(tk.INSERT, self.text.clipboard_get())
        
    def cut(self):
        self.copy()
        self.text.delete(tk.SEL_FIRST, tk.SEL_LAST)
        
    def replace(self):
        target = simpledialog.askstring("替换", "输入要替换的文本：")
        if target:
            replace_text = simpledialog.askstring("替换", "输入替换后的文本：")
            if replace_text:
                start = self.text.search(target, tk.INSERT, stopindex=tk.END)
                if start:
                    end = f"{start}+{len(target)}c"
                    self.text.delete(start, end)
                    self.text.insert(start, replace_text)
        
    def set_font(self):
        font = simpledialog.askstring("设置字体", "输入字体名称：")
        if font:
            self.text.config(font=(font, self.text['font'].split()[1]))
            
    def set_font_size(self):
        size = simpledialog.askinteger("设置字号", "输入字号：")
        if size:
            self.text.config(font=(self.text['font'].split()[0], size))
            
    def set_bg_color(self):
        color = colorchooser.askcolor(title="设置背景")
        if color[1]:
            self.text.config(bg=color[1])
        
    def set_fg_color(self):
        color = colorchooser.askcolor(title="设置字色")
        if color[1]:
            self.text.config(fg=color[1])
if __name__ == "__main__":
    root = tk.Tk()
    app = Notepad(root)
    root.mainloop()
```
代码大小4KB

>精简版
>同样用Python的IDLE新建

代码如下：
```python
import tkinter as tk
from tkinter import filedialog
def save_file():
    file_path = filedialog.asksaveasfilename()
    if file_path:
        with open(file_path, 'w') as file:
            file.write(text_editor.get('1.0', tk.END))
root = tk.Tk()
root.title()
menu_bar = tk.Menu(root)
root.config(menu=menu_bar)
file_menu = tk.Menu(menu_bar, tearoff=0)
menu_bar.add_cascade(label="保存", command=save_file)
text_editor = tk.Text(root)
text_editor.pack(expand=1, fill=tk.BOTH)
root.mainloop()
```
代码大小510字节！

>大小释义
>1KB=1024字节，510字节≈0.5KB！

>2024.7.22更新
>增加彩色代码高亮显示

OVER