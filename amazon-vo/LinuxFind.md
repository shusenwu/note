实现linux file find， 支持同时search by size, search by suffix, search的时候给定一个deep层数。 

```python
# -*- coding: UTF-8 -*-
# __author__ = 'Sengo'
from collections import defaultdict


class Folder(object):
    def __init__(self):
        self.children = defaultdict(Folder)
        self.createDate = ""
        self.user = ""
        self.group = ""
        self.hidden = False
        # and so on
        

class File:
    def __init__(self):
        self.fileName = ""
        self.content = ""
        self.size = 0
        self.fileType = ""
        self.createDate = ""
        self.lastModifyDate = ""
        self.hidden = False
        self.readOnly = False
        self.createUser = ""
        self.group = ""


class FileSearchSystem(object):
    def __init__(self):
        self.root = Folder()

    def find_file(self, path, deep=0, suffix="", sizeSmaller=0, sizeLarger=0):  # find and return folder or file at path.
        cur = self.root
        result_files = []

        if path == "/" and deep == 0:  # / root path 下的所有文件
            result_files = search_file_in_current_folder(cur, suffix, sizeSmaller, sizeLarger)

        elif path and deep == 0:
            # go to the deepest path, if it is a folder, return all files under it, if it is a file, return the file
            for folder in path.split("/")[1:]:
                cur = cur.children[folder]

            if isinstance(cur, Folder):
                # return all files under this folder
                result_files = search_file_in_current_folder(cur, suffix, sizeSmaller, sizeLarger)
            else:
                result_files.append(cur)

        elif path and deep > 0:  # find all files with a deep from the current path like 3
            for folder in path.split("/")[1:]:  # go to the current path first
                cur = cur.children[folder]
            # BFS the folder layer by layer
            cur_layer_folders = [cur]
            for i in range(deep):
                next_layer_folders = []
                for _folder in cur_layer_folders:
                    result_files += search_file_in_current_folder(_folder, suffix, sizeSmaller, sizeLarger)
                    next_layer_folders += search_folder_in_current_folder(_folder)
                cur_layer_folders = next_layer_folders

        # TODO return result_files with details the user want


def search_file_in_current_folder(folder, suffix="", sizeSmaller=0, sizeLarger=0):
    re = []
    for child in folder.children:
        if isinstance(child, File) and check_suffix(child, suffix) and check_sizeLarger(child, sizeLarger)\  # Or customer metho
                and check_sizeSmaller(child, sizeSmaller):
            re.append(child)
    return re


def search_folder_in_current_folder(folder):
    re = []
    for child in folder.children:
        if isinstance(child, Folder):
            re.append(child)
    return re


def check_suffix(file, suffix):
    if suffix == "" or file.name.endswith(suffix):
        return True
    return False


def check_sizeLarger(file, sizeLarger):
    if sizeLarger == 0 or file.size > sizeLarger:
        return True


def check_sizeSmaller(file, sizeSmaller):
    if sizeSmaller == 0 or file.size < sizeSmaller:
        return True


def check_prefix(file, prefix):  # We can also have other filter like prefix etc
    pass


```
