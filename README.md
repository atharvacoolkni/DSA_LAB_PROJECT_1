File System Simulation - README
This project implements a simple, in-memory file system simulation using modified trees and hash tables. It provides a CLI for users to interact with directories and files, much like a UNIX shell.

Data Structures Used
1. Modified Tree Structure (Directory Tree)
The directory structure is represented as a tree, where each directory is a node, and files and subdirectories are children of those nodes. Each directory node contains:

name: The name of the directory (or file).
parent: A pointer to the parent directory.
files: A hash table mapping file names to File objects.
subDirs: A hash table mapping directory names to child Directory objects.
The tree structure allows for efficient traversal between directories, making directory navigation operations like cd and ls fast and intuitive.

2. Modified Hash Tables (unordered_map)
*files (unordered_map<string, File>)**: Each directory maintains a hash table (unordered_map) of files where the keys are file names, and the values are pointers to File objects. This allows for quick lookups when searching for files within a directory.
*subDirs (unordered_map<string, Directory>)**: Each directory also maintains a hash table of subdirectories where the keys are directory names, and the values are pointers to Directory objects. This allows for quick lookups when navigating or managing subdirectories.
Class Breakdown
File Class
Represents a file in the file system.
Attributes:
name: Name of the file.
content: Content of the file (default is empty).
Usage: The File object is used for storing file-specific data, and it is stored within the files hash table of a Directory.
Directory Class
Represents a directory in the file system.
Attributes:
name: Name of the directory.
files: A hash table (unordered_map) storing File objects within the directory.
subDirs: A hash table (unordered_map) storing child Directory objects.
parent: Pointer to the parent Directory object.
Usage: The Directory class is used to organize files and other directories in a tree structure, and hash tables are used to efficiently store and retrieve files and subdirectories.
FileSystem Class
The main class managing the entire file system, operations like creating, reading, deleting files and directories, and navigating between directories.
Usage: The FileSystem class leverages the directory tree and hash tables to handle file system operations.
How Each Function Uses Data Structures
File Operations
createFile(string fileName, string content = "")

How it works:
Checks if the file already exists in the current directory using the files hash table.
If it doesn't exist, it creates a new File object and adds it to the files hash table in the current directory.
Data Structure Usage:
The function directly interacts with the unordered_map<string, File*> files in the Directory class to store and check for the file's existence.
readFile(string fileName)

How it works:
Looks for the file by its name in the files hash table of the current directory.
If found, it prints the file's content.
Data Structure Usage:
This function performs a lookup in the files hash table of the current directory to retrieve the File object and access its content.
deleteFile(string fileName)

How it works:
Looks for the file by name in the files hash table of the current directory.
If found, it deletes the file from the hash table and frees its memory.
Data Structure Usage:
It removes the file from the files hash table of the current directory and deallocates the File object.
Directory Operations
createDirectory(string dirName)

How it works:
Checks if the directory already exists using the subDirs hash table of the current directory.
If it doesn't exist, it creates a new Directory object and adds it to the subDirs hash table.
Data Structure Usage:
The unordered_map<string, Directory*> subDirs in the current directory is used to store and check for the existence of the subdirectory.
deleteDirectory(string dirName)

How it works:
Looks for the directory in the subDirs hash table of the current directory.
If found, it checks if the directory is empty (no files or subdirectories).
If empty, it deletes the directory from subDirs and frees its memory.
Data Structure Usage:
This function interacts with the subDirs hash table to find the target directory and delete it if it's empty.
changeDirectory(string dirName)

How it works:
If the name is "..", it moves to the parent directory using the parent pointer.
If the name is /, it moves to the root directory.
Otherwise, it searches for the subdirectory in subDirs and updates currentDir to the target subdirectory.
Data Structure Usage:
The subDirs hash table is used to look up and navigate to subdirectories, and the parent pointer is used to move up the directory tree.
listDirectory()

How it works:
Lists both files and subdirectories in the current directory.
Uses the files hash table to list all files and the subDirs hash table to list all subdirectories.
Data Structure Usage:
Iterates over the files and subDirs hash tables of the current directory to print the contents.
printCurrentDirectory()

How it works:
Prints the full path of the current directory by traversing up the directory tree using the parent pointer.
Data Structure Usage:
Uses the parent pointers in the Directory objects to traverse upwards through the directory tree.
Utility Operations
saveToFile(const string& filename)

How it works:
Saves the entire file system (root directory and its contents) to a file by recursively traversing the directory tree.
For each directory, it writes the directory name, files (from the files hash table), and subdirectories (from the subDirs hash table).
Data Structure Usage:
The function recursively traverses the subDirs hash table for subdirectories and the files hash table for files in each directory to save the entire file system structure.
loadFromFile(const string& filename)

How it works:
Reads the file system structure from a file and reconstructs the tree by creating new Directory and File objects.
Each directory's files are loaded from the files section, and subdirectories are loaded into the subDirs hash table.
Data Structure Usage:
The function populates the files and subDirs hash tables in each directory by reading from the file.
search(string name, Directory dir, string currentPath)*

How it works:
Recursively searches through the directory and subdirectories for a file or directory that matches the specified name.
If a match is found, it prints the path of the matching file or directory.
Data Structure Usage:
The function uses the files and subDirs hash tables to search for files and subdirectories recursively.
printAllFromRoot()

How it works:
Recursively prints all files and directories starting from the root directory.
Uses printDirectoryRecursively() to traverse the entire tree.
Data Structure Usage:
Recursively accesses the files and subDirs hash tables to print every file and directory in the file system.
