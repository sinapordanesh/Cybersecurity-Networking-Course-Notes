# 21_Shutil Module

The Python shutil module provides a number of methods for performing high-level file and folder operations. Here are some of the most commonly used methods along with examples of how to use them:

### 1. copy(src, dst)

This method copies the file from the source path to the destination path. If the destination already exists, it will be overwritten.

```python
import shutil

# Example Usage
shutil.copy('/path/to/source/file', '/path/to/destination/folder')
```

### 2. copy2(src, dst)

This method is similar to copy() but preserves more metadata about the file, such as the creation and modification times.

```python
import shutil

# Example Usage
shutil.copy2('/path/to/source/file', '/path/to/destination/folder')
```

### 3. move(src, dst)

This method moves the file or folder from the source path to the destination path. If the destination already exists, it will be overwritten.

```python
import shutil

# Example Usage
shutil.move('/path/to/source/file', '/path/to/destination/folder')
```

### 4. rmtree(path)

This method removes the directory and all its contents (including subdirectories) recursively.

```python
import shutil

# Example Usage
shutil.rmtree('/path/to/folder/to/remove')
```

### 5. make_archive(base_name, format, root_dir)

This method creates an archive file (such as a ZIP or TAR file) of the files in the specified directory.

```python
import shutil

# Example Usage
shutil.make_archive('/path/to/archive', 'zip', '/path/to/directory/to/archive')
```

These are just a few examples of the many methods provided by the Python Shutil module. For more information about these methods and their parameters, you can refer to the official Python documentation.