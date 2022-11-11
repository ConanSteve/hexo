---
title: Python中删除文件的几种方法
date: 2022-04-21
author: 陌上人如玉
comments:
description:
keywords:
top_img:
cover:
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
tags: 
categories:
  [编程语言, Python]
---
# 删除文件
很多时候开发者需要删除文件。可能是他错误地创建了文件，或者不再需要该文件。无论出于何种原因，都有一些方法可以通过Python来删除文件，而无需手动查找文件并通过UI交互来进行删除操作。

使用Python删除文件有多种方法，但是最好的方法如下：

* `os.remove()`删除文件
* `os.unlink()`删除文件。它是 `remove()`方法的Unix名称。
* `shutil.rmtree()`删除目录及其下面所有内容。
* `pathlib.Path.unlink()`在Python 3.4及更高版本中用来删除单个文件 `pathlib`模块。

## **`os.remove()` 删除文件**

Python中的OS模块提供了与操作系统进行交互的功能。OS属于Python的标准实用程序模块。该模块提供了使用依赖于操作系统的功能的便携式方法。

Python中的 `os.remove()`方法用于删除文件路径。此方法无法删除目录。如果指定的路径是目录，则该方法将引发 `OSError`。

注意：可以使用 `os.rmdir()`删除目录。

**句法：**

以下是 `remove()`方法删除Python文件的语法：

```
os.remove(path)
```

* `path` —— 这是要删除的路径或文件名。

**返回值**

`remove()`方法没有返回值。

我们来看一些使用 `os.remove`函数删除Python文件的示例。

**示例1：使用** ** `OS.Remove()` 方法删除文件的基本示例。**

```python
# Importing the os library
import os

# Inbuilt function to remove files
os.remove("test_file.txt")
print("File removed successfully")
```

**输出：**

```
File removed successfully
```

说明：在上面的示例中，我们删除了文件或删除了名为 `testfile.txt`的文件的路径。解释程序流程的步骤如下：

1.首先，我们导入了os库，因为os库中存在 `remove()`方法。
2.然后，我们使用内置函数 `os.remove()`删除文件的路径。
3.在此示例中，我们的示例文件是 `test_file.txt`。您可以在此处放置所需的文件。

注意：如果没有名为 `test_file.txt`的文件，则上面的示例将引发错误。因此，最好在删除文件之前先检查文件是否可用。

**示例2：使用** ** `os.path.isfile` 检查文件是否存在并使用 `os.Remove` 删除它**

在示例1中，我们刚刚删除了目录中存在的文件。 `os.remove()`方法将在工作目录中搜索要删除的文件。因此，最好检查文件是否存在。

让我们学习如何检查具有特定名称的文件在该路径中是否可用。我们正在使用 `os.path.isfile`来检查文件的可用性。

```python
#importing the os Library
import os

#checking if file exist or not
if(os.path.isfile("test.txt")):

    #os.remove() function to remove the file
    os.remove("demo.txt")

    #Printing the confirmation message of deletion
    print("File Deleted successfully")
else:
print("File does not exist")
#Showing the message instead of throwig an error
```

**输出：**

```
File Deleted successfully
```

在上面的示例中，我们仅添加了 `os.pasth.isfile()`方法。这种方法有助于我们找出文件是否存在于特定位置。

**示例3：Python程序删除具有特定扩展名的所有文件**

```python
import os
from os import listdir
my_path = 'C:\Python Pool\Test\'

for file_name in listdir(my_path):

    if file_name.endswith('.txt'):

        os.remove(my_path + file_name)
```

**输出：**

使用此程序，我们将从文件夹删除扩展名为 `.txt`的所有文件。

**解释：**

* 从os模块导入os模块和 `listdir`。必须使用 `listdir`才能获取特定文件夹中所有文件的列表，并且需要os模块才能删除文件。
* `my_path`是包含所有文件的文件夹的路径。
* 我们正在遍历给定文件夹中的文件。 `listdir`用于获取特定文件夹中所有文件的一个列表。
* `endswith`用于检查文件是否以 `.txt`扩展名结尾。当我们删除文件夹中的所有 `.txt`文件时，如果条件可以验证，则进行此操作。
* 如果文件名以 `.txt`扩展名结尾，我们将使用 `os.remove()`函数删除该文件。此函数将文件的路径作为参数。 `my_path` + `file_name`是我们要删除的文件的完整路径。

**示例4：删除文件夹中所有文件的Python程序**

要删除特定目录中的所有文件，只需使用 `*`符号作为模式字符串。

```python
#Importing os and glob modules
import os, glob

#Loop Through the folder projects all files and deleting them one by one
for file in glob.glob("pythonpool/*"):
    os.remove(file)
    print("Deleted " + str(file))
```

**输出：**

```
Deleted pythonpool\test1.txt
Deleted pythonpool\test2.txt
Deleted pythonpool\test3.txt
Deleted pythonpool\test4.txt
```

在此示例中，我们将删除 `pythonpool`文件夹中的所有文件。

注意：如果文件夹包含其他子文件夹，则可能会报错，因为 `glob.glob()`方法将获取所有文件夹内容的名称，无论它们是文件还是子文件夹。因此，请尝试使模式更具体（例如 `*.*`），以仅获取具有扩展名的内容。

## **使用`os.unlink()` 删除Python文件**

`os.unlink()`是 `os.remove()`的别名。在Unix OS中，删除也称为 `unlink`。

注意：所有功能和语法与 `os.unlink()`和 `os.remove()`相同。它们都用于删除Python文件路径。两者都是Python标准库的os模块中执行删除功能的方法。

它有两个名称，别名： `os.unlink()`和 `os.remove()`

为同一个函数提供两个别名的可能原因是，该模块的维护者认为，许多程序员可能会从C的底层编程转向Python，其中库函数和底层系统调用称为 `unlink()`，而其他人则可能会使用 `rm`命令（"删除"的缩写）或shell脚本来简化语言。

## **使用`shutil.rmtree()` 删除Python文件**

`shutil.rmtree()`：删除指定的目录，所有子目录和所有文件。此功能特别危险，因为它无需检查即可删除所有内容。结果，您可以使用此功能轻松丢失数据。

`rmtree()`是shutil模块下的一种方法，该方法以递归方式删除目录及其内容。

**句法：**

```
shutil.rmtree（path，ignore_errors = False，onerror = None）
```

**参数：**

`path`：类似路径的对象，表示文件路径。类路径对象是表示路径的字符串或字节对象。

`ignore_errors`：如果 `ignore_errors`为 `true`，则删除失败导致的错误将被忽略。

`oneerror`：如果 `ignore_errors`为 `false`或被忽略，则通过调用 `onerror`指定的处理程序来处理此类错误。

我们来看一个使用python脚本删除文件的示例。

示例：使用 `Shutil.Rmtree()`删除文件的Python程序

```python
# Python program to demonstrate shutil.rmtree()

import shutil
import os

# location
location = "E:/Projects/PythonPool/"

# directory
dir = "Test"

# path
path = os.path.join(location, dir)

# removing directory
shutil.rmtree(path)
```

**输出：**

它将删除Test内文件的整个目录，包括Test文件夹本身。

## **Python中使用`pathlib.Path.unlink()` 删除文件**

`pathlib`模块在Python 3.4及更高版本中可用。如果要在Python 2中使用此模块，可以使用pip进行安装。 `pathlib`提供了一个面向对象的界面，用于处理不同操作系统的文件系统路径。

要使用 `pathlib`模块删除文件，请创建一个指向该文件的 `Path`对象，然后对该对象调用 `unlink&#xFF08;&#xFF09;`方法：

**示例：使用** ** `Pathlib` 删除文件的Python程序**

```python
#Example of file deletion by pathlib

import pathlib

rem_file = pathlib.Path("pythonpool/testfile.txt")

rem_file.unlink()
```

在上面的示例中， `path()`方法用于检索文件路径，而 `unlink()`方法用于删除指定路径的文件。

`unlink()`方法适用于文件。如果指定了目录，则会引发 `OSError`。要删除目录，我们可以采用前面讨论的方法之一。

在本文中，我们学习了Python删除文件的各种方法。使用Python删除文件或文件夹的语法非常简单。但是，请注意，一旦执行上述命令，您的文件或文件夹将被永久删除。

# 重命名文件
重命名文件和文件夹名称都可以
```python
os.rename("old file path", "new file path")
```