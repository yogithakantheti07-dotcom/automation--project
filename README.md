# automation--project
import os
import shutil
from datetime import datetime

# Log function

def write_log(message):
    with open("logs.txt", "a") as log:
        log.write(f"{datetime.now()} - {message}\n")

# Organize files by extension

def organize_files(folder_path):
    try:
        files = os.listdir(folder_path)

        for file in files:
            file_path = os.path.join(folder_path, file)

            if os.path.isfile(file_path):
                extension = file.split('.')[-1]
                extension_folder = os.path.join(folder_path, extension)

                if not os.path.exists(extension_folder):
                    os.makedirs(extension_folder)

                shutil.move(file_path, os.path.join(extension_folder, file))
                write_log(f"Moved {file} to {extension_folder}")

        print("Files organized successfully!")

    except Exception as e:
        write_log(f"Error: {e}")
        print("An error occurred.")

# User Input
folder = input("Enter folder path: ")
organize_files(folder)