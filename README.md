import os
import re

# Define a list of malicious patterns (for demonstration purposes)
malicious_patterns = [r'virus', r'malware', r'trojan']

def is_malicious(file_path):
    with open(file_path, 'r', errors='ignore') as file:
        content = file.read()
        for pattern in malicious_patterns:
            if re.search(pattern, content):
                return True
    return False

def scan_and_delete(directory):
    for root, dirs, files in os.walk(directory):
        for file in files:
            file_path = os.path.join(root, file)
            if is_malicious(file_path):
                print(f"Malicious file detected and deleted: {file_path}")
                os.remove(file_path)

if __name__ == "__main__":
    directory_to_scan = input("Enter the directory to scan: ")
    scan_and_delete(directory_to_scan)
    
