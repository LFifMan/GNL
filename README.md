# Get Next Line (GNL) 🎉

## Overview 🌟

Welcome to the Get Next Line project! This utility is designed to help you read lines from a file descriptor effortlessly. It's particularly useful for C programmers who want to handle file input line by line without getting bogged down by low-level details like buffering and string manipulation.

## Files in the Project 📂

- get_next_line.c: The heart of the project, containing the main logic for reading lines from a file descriptor.
- get_next_line_utils.c: Utility functions that support the main logic, such as memory allocation, string manipulation, and buffer management.
- get_next_line.h: Header file declaring the functions used in the project, along with necessary libraries and constants.

## Detailed Description of Files 📄

#### get_next_line.c:

- get_next_line(int fd): Reads the next line from the given file descriptor fd. Uses static storage for tracking any leftover data between calls.
- ft_readfile(char *buffer, int fd): Reads data from the file descriptor into the buffer.
- ft_prepline(char *buffer): Prepares the next line by locating the newline character.
- ft_delreadline(char *buffer): Updates the buffer by removing the line that was just read.
- ft_joinandfree(char *buffer, char *tmpbuff): Joins two buffers and frees the temporary buffer for efficient memory management.

#### get_next_line_utils.c:

- ft_calloc(size_t count, size_t size): Allocates memory and initializes it to zero.
- ft_bzero(void *str, size_t size): Sets a block of memory to zero.
- ft_strchr(char *str, int c): Locates the first occurrence of a character in a string.
- ft_strlen(char *str): Computes the length of a string.
- ft_strjoin(char *buffer, char *tmpbuff): Concatenates two strings.

#### get_next_line.h:

Declares prototypes for all functions and includes necessary libraries and constants.

## How It Works ⚙️

Initialization: Call get_next_line with a file descriptor. If it's the first call, the buffer is initialized to handle data read from the file.
Reading Data: ft_readfile reads data from the file descriptor into a buffer. It handles end-of-file and error cases appropriately.
Processing Lines: ft_prepline processes the buffer to find the next line, separated by a newline character. The line is then prepared for return.
Updating Buffer: After a line is read, ft_delreadline updates the buffer by removing the processed data, allowing subsequent calls to get_next_line to continue reading from where it left off.
Memory Management: Uses functions like ft_calloc, ft_bzero, and ft_joinandfree to manage memory efficiently, ensuring no leaks and proper resizing and cleanup of the buffer.

## Usage 🚀

To use this utility in your project, include the get_next_line.h header and call the get_next_line function with a valid file descriptor. It returns a string containing the next line from the file each time it is called, or NULL if there are no more lines or an error occurs.

```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main() {
    int fd = open("example.txt", O_RDONLY);
    char *line;

    while ((line = get_next_line(fd)) != NULL) {
        printf("%s\n", line);
        free(line);
    }

    close(fd);
    return 0;
}
```
This example opens a file, reads it line by line using get_next_line, prints each line, and frees the allocated memory.
